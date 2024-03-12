# 01 basic

## 数据类型

![数据类型](./assets/01数据类型.png)

### 基本数据类型

| 基本类型 | 位数 | 字节 | 默认值 | 取值范围 |
| --- | --- | --- | --- | --- |
| byte | 8 | 1 | 0 | -128 ~ 127 |
| short | 16 | 2 | 0 | -32768 ~ 32767 |
| int | 32 | 4 | 0 | -2147483648 ~ 2147483647 |
| long | 64 | 8 | 0L | -9223372036854775808 ~ 9223372036854775807 |
| char | 16 | 2 | 'u0000' | 0 ~ 65535 |
| float | 32 | 4 | 0f | 1.4E-45 ~ 3.4028235E38 |
| double | 64 | 8 | 0d | 4.9E-324 ~ 1.7976931348623157E308 |
| boolean | 1 |  | false | true、false |

### 包装类

基本类型都有对应的包装类型，基本类型与其对应的包装类型之间的赋值使用自动装箱与拆箱完成。

```java
Integer x = 2;     // 装箱
int y = x;         // 拆箱
```

- new Integer(123) 每次都会新建一个对象
- Integer.valueOf(123) 会使用缓存池中的对象，多次调用会取得同一个对象的引用。

```java
Integer a= new Integer(123);
Integer b = new Integer(123);
System.out.println(a == b);    // false
Integer c = Integer.valueOf(123);
Integer d = Integer.valueOf(123);
System.out.println(c == d);   // true
```

编译器会**在缓冲池范围内的基本类型**自动装箱过程调用 valueOf() 方法，因此多个 Integer 实例使用自动装箱来创建并且值相同，那么就会引用相同的对象

```java
    public static Integer valueOf(int i) {
        if (i >= IntegerCache.low && i <= IntegerCache.high)
            return IntegerCache.cache[i + (-IntegerCache.low)];
        return new Integer(i);
    }

    private static class IntegerCache {
        static final int low = -128;
        static final int high;
        static final Integer cache[];

        static {
            // high value may be configured by property
            int h = 127;
            String integerCacheHighPropValue =
                sun.misc.VM.getSavedProperty("java.lang.Integer.IntegerCache.high");
            if (integerCacheHighPropValue != null) {
                try {
                    int i = parseInt(integerCacheHighPropValue);
                    i = Math.max(i, 127);
                    // Maximum array size is Integer.MAX_VALUE
                    h = Math.min(i, Integer.MAX_VALUE - (-low) -1);
                } catch( NumberFormatException nfe) {
                    // If the property cannot be parsed into an int, ignore it.
                }
            }
            high = h;

            cache = new Integer[(high - low) + 1];
            int j = low;
            for(int k = 0; k < cache.length; k++)
                cache[k] = new Integer(j++);

            // range [-128, 127] must be interned (JLS7 5.1.7)
            assert IntegerCache.high >= 127;
        }

        private IntegerCache() {}
    }
```

基本类型对应的缓冲池如下:

- boolean values true and false
- all byte values
- short values between -128 and 127
- int values between -128 and 127
- char in the range \u0000 to \u007F

### 基本数据和包装类

- 基本类型占用的空间更小
- 基本类型不赋值有默认值，而包装类型不赋值默认为null
- 基本类型存储在栈中，包装类型存储在堆中
    - Java中的基本类型（如**`int`**、**`float`**、**`double`**、**`boolean`**等）通常存储在栈内存中。这是因为基本类型的值直接存储在使用它们的方法的栈帧中。基本类型的值是直接按值传递的，它们的生命周期通常随着方法的调用而开始，随着方法的返回而结束
    - 另一方面，包装类型（如**`Integer`**、**`Float`**、**`Double`**、**`Boolean`**等）是基本类型的对象表示形式，它们用于Java集合框架中，以及在需要对象而非基本类型的其他情况下。由于包装类型是对象，它们的实例存储在堆内存中。当创建一个包装类型的实例时（例如通过**`new Integer(5)`**），就会在堆内存中分配空间来存储这个对象，而对象的引用则可以存储在栈内存中（如果它是一个局部变量）。
- 无论是基本类型还是引用类型的成员变量，如果它们是对象的非**`static`**成员，那么这些成员变量的数据都存储在堆内存中的。
    - static变量是存储在方法区的

### 自动装箱和拆箱

```java
Integer c1 = 33;//装箱
        int c2 = c1;//拆箱
```

![unboxing](./assets/02unboxing.png)

从字节码中，我们发现装箱其实就是调用了 包装类的`valueOf()`方法，拆箱其实就是调用了 `xxxValue()`方法。

### scene

- **场景一、将基本数据类型放入集合类**

Java中的集合类只能接收对象类型

```java
List<Integer> li = new ArrayList<>();
 for (int i = 1; i < 50; i ++){  
    li.add(i); 
    }
    
 反编译
         List<Integer> li = new ArrayList<>();
        for (int i = 1; i < 50; i++) {
            li.add(Integer.valueOf(i));
        }
```

- **场景二、包装类型和基本类型的大小比较**

对Integer对象与基本类型

```java
Integer a=1;
 System.out.println(a==1?"等于":"不等于");
 Boolean bool=false; 
 System.out.println(bool?"真":"假");
 ----------------------------------------------------
         Integer a = 1;
        System.out.println(a.intValue() == 1 ? "等于" : "不等于");
        Boolean bool = false;
        System.out.println(bool.booleanValue() ? "真" : "假");
```

包装类与基本数据类型进行比较运算，是先将包装类进行拆箱成基本数据类型，然后进行比较的。

- **场景三、包装类型的运算**

对Integer对象进行四则运算

```java
Integer i = 10; Integer j = 20; System.out.println(i+j);
--------------------------------------------------------
        Integer i2 = 10;
        Integer j = 20;
        System.out.println(i2.intValue() + j.intValue());
```

两个包装类型之间的运算，会被自动拆箱成基本类型进行。

- **场景四、三目运算符的使用**

```java
boolean flag = true; 
Integer i = 0;
 int j = 1; 
 int k = flag ? i : j;
--------------------------------------------------------
        Integer i = 0;
        int k = 1 != 0 ? i.intValue() : 1;
        System.out.println(k);
```

这是三目运算符的语法规范：当第二，第三位操作数分别为基本类型和对象时，其中的对象就会拆箱为基本类型进行操作。

因为例子中，flag ? i : j;片段中，第二段的i是一个包装类型的对象，而第三段的j是一个基本类型，所以会对包装类进行自动拆箱。如果这个时候i的值为null，那么就会发生NPE。

![npe](./assets/03unboxingscene.png)

### 引用类型

## 操作符