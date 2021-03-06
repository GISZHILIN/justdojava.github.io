---
layout: post  
title: Java Grammar：运算符
tagline: by Vi的技术博客
categories: java基础 
tags: 
    - Vi的技术博客

---

Java中的运算符
<!--more-->

### 简介

修饰符是用于限定类型以及类型成员申明的一种符号，从修饰对象上可以分为类修饰符，方法修饰符，变量修饰符；从功能上可以划分为访问控制修饰符和非访问修饰符。访问修饰符控制访问权限，不同的访问修饰符有不同的权限范围，而非访问修饰符则是提供一些特有功能。  

![image-20190812210957757](http://www.justdojava.com/assets/images/2019/java/image_vi/08_17/2019-08-17-1.png)

下面我们从功能的角度分别讲解修饰符



### 访问修饰符

访问修饰符有四种：`public`,`private`,`protected`,`default`。这里需要注意，我们这里的`default`和非访问修饰符中的`default`可不是一个东西！

这里的`default`指的是默认，**什么也不写**，在同一包内可见，不使用任何修饰符。使用对象：**类、接口、变量、方法**。

`private`指的是在仅仅在类内可见，所以也就很好理解，`private`只能修饰**方法，变量**，而不能修饰类和接口（毕竟你只能类内访问，你修饰类谁能看得到呢？），修饰方法的时候，一般用于我们在重构代码的时候提取公用代码为**内部实现方法**，修饰变量的情景相比我们就经常见到了，由于Java的**封装**特性，我们在定义一个类的时候，经常会把该类的属性定义为`private`，通过`get`or`set`方法来访问这些变量。

而`public`在我们日常中使用的比较多，我们经常会把类声明为`public`，声明成`public`的**类，接口，变量，方法**可以被任何类访问，这里需要注意一个java文件中只能包含一个`public`的类，而且`main`方法必须用`public`修饰，否则无法被Java的解释器识别。

`protected`我们在日常的开发中使用不多，只能声明在**变量，方法，内部类**上，它主要的作用就是用来**保护子类**的。它的含义在于子类可以用它修饰的成员，其他的不可以，它相当于传递给子类的一种**继承**的东西。

- 基类的 `protected` 成员是包内可见的，并且**对子类可见**；
- 若子类与基类不在同一包中，那么在子类中，子类实例**可以访问**其从**基类继承而来**的`protected`方法，而**不能访问基类实例**的`protected`方法。

![image-20190812221038073](http://www.justdojava.com/assets/images/2019/java/image_vi/08_17/2019-08-12-141038.png)

⬆ 大概就是上图酱紫，凑合着看，画图功力贼差：）



### 非访问修饰符

#### default

这里的`default`是jdk 8中的新特性，指的是接口方法的默认实现，在JDK 8 之前接口的方法是不能有实现的，而JDK 8 后`default`修饰的方法可以在接口中进行默认的实现：

```java
public interface Test {
  default void hello(){
    System.out.println("Hello");
  }
}
```

就像酱紫~

#### static

static是面试的一个**热点**，static的意思是静态，可用于修饰变量和方法，切记一点，static是属于**类**的，而非是属于对象的，static关键字修饰的方法或者变量不需要依赖于对象来进行访问，只要类被加载了，就可以通过**类名**去进行访问。
而static关键字的基本作用就是：方便在没有创建对象的情况下来进行调用（方法/变量）。
这里需要注意，由于static修饰的方法和变量是属于类的，不需要依靠对象才能使用，所以他不能访问非static修饰的方法和变量，因为这些变量和方法是必须依托于对象才能访问！但是**非static的方法可以访问static的方法或变量**，因为当你创建对象的时候，类必定已经加载，所以可以访问的到。

这里需要注意一点：static不可修饰局部变量

#### final

`final`关键字我们在日常中也会经常用到，通常用的最多的场景就是搭配`static`一起来使用去定义我们系统的常量：

```java
public static final String AUTHOR = "viyoung"
```

除了修饰变量，还可以用于修饰类和方法，被final修饰的类无法被继承，**被final修饰的方法可以被继承，但是无法进行修改**。



#### abstract

`abstract`可以作用在类和方法上，当作用在类上时，说明这个类是一个抽象类，需要去继承扩展，无法直接实例化一个对象，当作用在方法上的时候，说明这个方法需要扩展，被`abstract`修饰的方法以分号结尾，没有实现，而且无法被`final`和`static`修饰（一个需要被继承且没有实现的方法为毛要用这俩修饰，不是自己打自己脸吗😂）：

```java
abstract void test();
```

抽象类和抽象方法有以下关系：**包括抽象方法的一定是抽象类，不包括抽象方法的却不一定是非抽象类。**🤔



#### synchronized

`synchronized`对于了解过并发编程的同学来说比较熟悉，它可以作用于普通方法，static方法和代码块上，用于加锁，放置多个线程同时访问一个方法/类。这里只是简单的介绍，会在后面的并发编程中详细讲解。



#### volatile

`volatile` 修饰的成员变量具有**可见性**，**可见性，是指线程之间的可见性，一个线程修改的状态对另一个线程是可见的。**也就是一个线程修改的结果。另一个线程马上就能看到。比如：用volatile修饰的变量，就会具有可见性。volatile修饰的变量不允许**线程内部缓存和重排序**，即直接修改内存。

这里也只是简单的介绍，会在后面的并发编程中详细讲解。



#### transient

用**transient**关键字标记的成员变量不参与序列化过程，Java的serialization提供了一种持久化对象实例的机制。当持久化对象时，可能有一个特殊的对象数据成员，我们不想用serialization机制来保存它。为了在一个特定对象的一个域上关闭serialization，可以在这个域前加上关键字transient。当一个对象被序列化的时候，transient型变量的值不包括在序列化的表示中，然而非transient型的变量是被包括进去的。

```java
private transient String name = "viyoung";
```