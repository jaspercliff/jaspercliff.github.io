# 02 object-oriented
## encapsulation extends polymorphism

有助于构建模块化、可维护和可扩展的代码

## encapsulation

利用抽象数据类型将数据和对数据的操作封装在一起，用户不需要知道对象内部的操作，但是可以通过对象提供的对外接口访问该对象
- advantage
- 减少耦合 独立的开发 测试 使用
- 提高软件的可重用性

## extends

cat extends Animal 可以获得animal的非private属性和方法

``` java
Animal animal = new Dog()
```

遵循里氏代换原则，子类对象可以替换掉所有父类对象

## polymorphism

不同的对象对同一消息作出不同的响应

- 编译时多态
    - overloading
    - 方法的重载
- 运行时多态
    - extends override 向上转型
    - 定义的对象引用 在运行期间才能确定具体的类型
  
## 类为什么要有无参构造器
在Java中，类有无参构造器（也称为默认构造器）的原因和好处主要包括以下几点：

- 简化对象的创建
当类中没有显式定义任何构造器时，Java编译器会自动提供一个无参构造器。这样做的目的是为了简化那些不需要特殊初始化的对象的创建过程。如果没有这个默认的无参构造器，而你又需要创建对象，就必须显式定义至少一个构造器。
- 便于继承
在Java的继承机制中，子类的构造器会隐式或显式地调用父类的无参构造器（如果父类没有无参构造器，就必须显式调用父类的其他构造器）。如果父类没有无参构造器（且没有显式定义任何构造器），子类的构造器就会编译失败，除非显式地通过`super`关键字调用父类的其他构造器。因此，无参构造器在继承体系中起到了桥梁的作用。
- 灵活性和扩展性
有时候，类的设计初期可能不需要任何特殊的构造逻辑，所以没有定义具有参数的构造器。随着类的发展，可能会添加更多的属性和方法，但是仍然需要保留无参构造器来提供对象的简单实例化方式。无参构造器提供了一种灵活和可扩展的方式来创建对象，即使以后类的设计发生了变化。
-  兼容性
某些Java框架和库（如Spring和Hibernate）在创建类的实例时依赖于无参构造器。这些框架使用反射来创建对象的实例，而反射机制需要无参构造器。如果没有无参构造器，这些框架可能无法正确地创建对象实例，导致运行时错误。
   序列化和反序列化
在Java序列化中，当反序列化对象时，JVM需要调用类的无参构造器来创建对象。如果类没有无参构造器，反序列化过程可能会失败。

综上所述，无参构造器在Java编程中非常重要，它提供了对象创建、继承、框架兼容性、序列化支持等方面的便利和灵活性。即使在某些情况下你不需要无参构造器，了解它的存在和目的仍然对编写健壮、灵活的Java代码非常有帮助。

## class and object 类和对象
- 类是一个模板或蓝图，用于定义对象的结构和行为。它是一个抽象概念，不占用任何内存空间。类定义了一组属性（字段、变量）和方法（函数、操作），这些属性和方法共同定义了该类的对象的状态和行为。
- 对象是类的实例。当根据类模板创建一个新实例时，就产生了一个对象。对象占用内存空间，并具有实际的状态和行为。每个对象都有其自己的属性值，这些值是该对象的状态的一部分。对象可以调用定义在其类中的方法来执行操作
## abstract class
在Java中，抽象类是一种特殊的类，它不能被实例化，即你不能直接创建抽象类的对象。抽象类的主要目的是作为其他类的超类（父类），提供一个基本的框架，让子类继承并实现抽象方法，以此来拥有更具体的功能。以下是关于抽象类的一些关键点：

### 定义抽象类
使用`abstract`关键字来声明抽象类。抽象类可以包含抽象方法（没有具体实现的方法，也使用`abstract`关键字声明）和具体方法（有具体实现的方法）。

```java
abstract class Animal {
    abstract void makeSound();

    void breathe() {
        System.out.println("Animal is breathing.");
    }
}
```

在这个例子中，`Animal`是一个抽象类，其中`makeSound()`是一个抽象方法，而`breathe()`是一个具体的实现方法。

### 抽象方法
抽象方法是只有声明而没有具体实现的方法。它允许子类以各自不同的方式来实现这些方法。如果一个类包含至少一个抽象方法，那么这个类必须被声明为抽象类。

### 抽象类的继承
当一个非抽象类继承自抽象类时，它必须实现父类中的所有抽象方法。否则，这个类也必须被声明为抽象类。

```java
class Dog extends Animal {
    void makeSound() {
        System.out.println("Woof");
    }
}
```

在这个例子中，`Dog`类继承自`Animal`类，并实现了`makeSound()`方法。

### 使用抽象类
尽管我们不能直接实例化抽象类，但它们可以作为引用类型。这意味着你可以使用抽象类类型的变量来引用其子类的对象。

``` java
Animal myDog = new Dog();
myDog.makeSound(); // 输出: Woof
myDog.breathe();   // 输出: Animal is breathing.
```

### 抽象类的用途
- **共享代码**：通过抽象类，可以在多个子类之间共享方法或数据字段。
- **设计框架和API**：抽象类允许你定义一个标准，子类必须遵守这个标准，这对于设计大型系统或框架非常有用。
- **强制子类实现特定方法**：抽象类可以强制要求子类实现特定的方法，确保子类具有抽象类定义的基本行为。

抽象类是Java面向对象编程中的一个核心概念，它提供了一种强大的方式来组织和模块化代码，同时促进了代码的重用。
## interface
接口字段默认是public static final的
```java
public interface MyInterface {
    // 声明一个public static final的字段
    int MAX_SIZE = 100;

    // 接口方法声明
    void myMethod();
}
```
## abstract class and interface
- 抽象类表示"是一个"的关系
- interface表示的是“能做什么” 定义的是行为规范
---
- 抽象类的方法可以使用private protected public修饰
- interface的方法只能是public的
---
- class 单继承
- interface 可以多继承
---
- 抽象类：可以包含抽象方法和具体方法，还可以声明**字段**和**构造函数**。
- 接口在Java 8之前，只能包含抽象方法；Java 8及以后，可以包含默认方法和静态方法。Java 9加入了私有方法。接口不能包含字段（除了静态和最终字段）
---
- 向抽象类添加新方法 会破坏子类
- 向interface可以添加默认方法 子类不需要实现 jdk8以后
如果你需要从多个类中共享代码，则使用抽象类。如果你需要定义一个能由多个无关类实现的合同，则使用接口

## Object
所有类的父类


## 内部类
Java内部类是定义在另一个类的内部的类。这种结构使得内部类能够访问其外部类的成员，包括私有成员。
内部类主要用于将一些逻辑紧密地封装在某个类的内部，而不是暴露给整个包。使用内部类可以使代码更加模块化和封装
Java内部类是定义在另一个类的内部的类。这种结构使得内部类能够访问其外部类的成员，包括私有成员。内部类主要用于将一些逻辑紧密地封装在某个类的内部，而不是暴露给整个包。使用内部类可以使代码更加模块化和封装。

内部类主要分为以下几种：

###  成员内部类（Non-static Nested Class）

成员内部类是最常见的内部类类型，它需要依附于外部类的对象实例。成员内部类可以无条件访问外部类的所有成员，包括私有成员。

``` java
public class OuterClass {
    private int value = 10;

    class InnerClass {
        public void printValue() {
            System.out.println("Value: " + value);
        }
    }
}
```

###  静态内部类（Static Nested Class）

静态内部类与成员内部类类似，但是被声明为静态（`static`）。静态内部类不需要外部类的对象实例就可以被创建。它不能直接访问外部类的实例成员，只能访问外部类的静态成员。

``` java
public class OuterClass {
    private static int value = 10;

    static class StaticInnerClass {
        public void printValue() {
            System.out.println("Value: " + value);
        }
    }
}
```

###  局部内部类（Local Inner Class）

局部内部类是在一个块内部（如方法或者任意作用域内）定义的类。它不同于成员内部类，因为它的作用域被限定在声明它的块中。

``` java
public class OuterClass {
    public void someMethod() {
        class LocalInnerClass {
            public void printMessage() {
                System.out.println("Inside someMethod");
            }
        }
        LocalInnerClass lic = new LocalInnerClass();
        lic.printMessage();
    }
}
```

###  匿名内部类（Anonymous Inner Class）

匿名内部类是没有名字的内部类，通常用于只需要使用一次的场景。它们通常用于接口或抽象类的实例化。

``` java
new Thread(new Runnable() {
    @Override
    public void run() {
        System.out.println("Anonymous Inner Class");
    }
}).start();
```

内部类的使用有助于使代码更加简洁且具有更好的封装性，但也增加了复杂性。合理使用内部类可以使设计更加灵活，更好地将实现细节隐藏起来。

[//]: # (### 合成构造函数)

[//]: # (在Java中，合成构造函数是由编译器自动生成的构造函数，主要用于在某些特定的场景下，)

[//]: # (如内部类访问其外部类的私有成员时，提供必要的访问权限。)

[//]: # (合成构造函数并不直接出现在源代码中，但在编译后的字节码中可以看到它们的存在)

[//]: # (``` java)

[//]: # (public class OuterClass {)

[//]: # (    private int privateField = 1;)

[//]: # ()
[//]: # (    private class InnerClass {)

[//]: # (        void show&#40;&#41; {)

[//]: # (            System.out.println&#40;"Accessing private field: " + privateField&#41;;)

[//]: # (        })

[//]: # (    })

[//]: # (})

[//]: # ()
[//]: # (```)

[//]: # (- OuterClass.class 是 OuterClass 这个外部类的编译结果。当你编译包含 OuterClass 的 .java 文件时，会生成这个 .class 文件。)

[//]: # (- OuterClass$InnerClass1.class 是 OuterClass 中定义的一个内部类 InnerClass1 的编译结果。在Java中，内部类被编译成它们自己的 .class 文件，)

[//]: # (这个文件的命名约定是 外部类名$内部类名.class。这样的命名表示 InnerClass1 是 OuterClass 的一个内部类。)
