# 枚举

是一个特殊的类 一般表示一组常量 比如一年四季

you should use enum types any time you need to represent a fixed set of constants

The enum declaration defines a *class* (called an *enum type*). The enum class body can include methods and other fields. The compiler automatically adds some special methods when it creates an enum. For example, they have a static values method that returns an array containing all of the values of the enum in the order they are declared. This method is commonly used in combination with the for-each construct to iterate over the values of an enum type. For example, this code from the Planet class example below iterates over all the planets in the solar system.

***All* enums implicitly extend
java.lang.Enum**

每一个枚举类型都可以看作是一个Enum的实例

Red 和 BLACK都有color属性

```java
 enum Color{
        RED("red"),BLACK("black");
        private final String color;
     // 构造方法必须是私有的
//如果允许外部程序创建新的枚举实例，就可能破坏枚举实例的唯一性和稳定性
        private Col**or(String color){
            this.color** = color;
        }
    }
    public static void main(String[] args) {
        System.out.println(Color.RED.color);
    }

output:red
```

but Enum 里面没有values方法

```java
package se.enum_study;
public class demo {
    enum Color{
        RED,BLUE,BLACK
    }
    public static void main(String[] args) {
        for (Color value : Color.values()) {
            System.out.println(value);
        }
    }
}

```

javap demo$Color.class

```java
  public static final se.enum_study.demo$Color BLUE;
  public static final se.enum_study.demo$Color BLACK;
  public static se.enum_study.demo$Color[] values();
  public static se.enum_study.demo$Color valueOf(java.lang.String);
  static {};
```

可以看到自动插入了 values方法

The compiler automatically adds some special methods when it creates an enum

枚举成员默认都被public static final 修饰

## methods

values 返回枚举类中所有的值

ordinal  找到每个枚举常量的值

vlaueof  返回指定字符串的枚举常量

**`name()`**方法是**`Enum`**类的一个内置方法，它返回枚举常量的名称作为一个字符串

```
    public static void main(String[] args) {
        for (Color value : Color.values()) {
            System.out.println(value.ordinal()+":"+value);
        }
        System.out.println(Color.valueOf("RED"));
```

枚举类中有抽象方法 则枚举类中的每个对象都对其进行实现

```
enum Color{
        RED{
            @Override
            public String getColor() {
                return "RED";
            }
        }
        ,BLUE{
            @Override
            public String getColor() {
                return "BLUE";
            }
        },BLACK{
            @Override
            public String getColor() {
                return "black";
            }
        };
```

## EnumMap

public class EnumMap<K extends Enum<K>,V>

extends AbstractMap<K,V>

implements Serializable, Cloneable

### class diagram

### constructor
1. the constructor is used to create an empty EnumMap with specified keyType
2. the constuctor is used to create an enum map with the same keyType as the specified enum map,with initial mappings being the sanme as the enum map
3. the constructor is used to create an enum map with initialization from the sprcified map in the parameter

### Example

```
public class EnumMapExample {
    public enum Color {
        RED,
        BLACK,
        BLUE;
    }

    public static void main(String[] args) {
        EnumMap<Color, String> enumMap = new EnumMap<>(Color.class);
        enumMap.put(Color.RED, "color is red");
        enumMap.put(Color.BLACK, "color is black");
        enumMap.put(Color.BLUE, "color is blue");
        System.out.println(enumMap.size());
        System.out.println(enumMap);
        System.out.println("key: " + Color.RED + " Value:" + enumMap.get(Color.RED));
        System.out.println("Does enumMap has " + Color.BLUE + " :" + enumMap.containsValue("color is red"));
        System.out.println("-----------------------------------");
        System.out.println("key/value mapping is " + enumMap.entrySet());
        System.out.println("keySet " + enumMap.keySet());
        System.out.println("values "+enumMap.values());
        System.out.println("----------");
        enumMap.replaceAll((key,oldValue) -> oldValue+"  jasper");
        System.out.println(enumMap.entrySet());
    }
}

output:
3
{RED=color is red, BLACK=color is black, BLUE=color is blue}
key: RED Value:color is red
Does enumMap has BLUE :true
-----------------------------------
key/value mapping is [RED=color is red, BLACK=color is black, BLUE=color is blue]
keySet [RED, BLACK, BLUE]
values [color is red, color is black, color is blue]
----------
[RED=color is red  jasper, BLACK=color is black  jasper, BLUE=color is blue  jasper]
```

```
replaceAll()
default void replaceAll(BiFunction<? super K, ? super V, ? extends V> function)
@FunctionalInterface  函数式编程
public interface BiFunction<T, U, R>
```

## EnumSet

public abstract class EnumSet<E extends Enum<E>>

extends AbstractSet<E>

implements Cloneable, Serializable