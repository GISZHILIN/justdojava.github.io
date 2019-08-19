---
layout: post  
title: Java Grammar：数据类型
tagline: by Vi的技术博客
categories: Java  
tag: 
    - Java

---

Java中的基础数据类型

<!--more-->

### Java的数据类型

我们知道，Java是一种**强类型**语言，类型对于Java语言来说非常的重要不言而喻，在Java中，分为**基础数据类型**和**引用数据类型**，其中基础数据类型分为了**四类八种**：

![](http://www.justdojava.com/assets/images/2019/java/image_vi/07_31/basedatatype.png)

下面，我们来分别说一下这四类八种

### 整形

首先，需要说明一点，在Java的整形中不存在`unsigned`类型的数值，也就是说Java的整形都是有符号的可为正，可为负的整数



| 名称 | 取值范围 |字节数|位数|包装类|
| --- | --- |---|---|---|
| byte | $-2^7$ 到 $2^7-1$ |1|8|Byte|
| short | $-2^{15}$ 到 $2^{15}-1$ |2|16|Short|
| int | $-2^{31}$ 到 $2^{31}-1$ |4|32|Integer|
| long |$-2^{63}$ 到 $2^{63}-1$  |8|64|Long|


可以看出，取值范围取决于该类型的位数，由于Java的代码是运行在JVM中，所以该类型是独立于机器之外存在的，与机器的关系并没有很大，大大的提高了代码的可移植性。

在书写代码的时候，我们需要注意，在我们定义一个`long`类型的变量时，一定要记得在代码后加上大写的**L**（小写的l在某些字体下容易被认证1，给代码的可读性带来影响）。

#### 整形默认类型

我们的整数默认类型是int类型，在我们进行计算的时候，会默认按照int类型进行计算。

```java
byte a = 127; //right

byte b = 1; //right

byte c = a + b; // wrong

byte d = 127 + 1; //wrong
```

编译器报错两处，均是下面的这个错误信息：

```
HelloWorld.java:7: 错误: 不兼容的类型: 从int转换到byte可能会有损失
byte c = a + b; // wrong
           ^
HelloWorld.java:9: 错误: 不兼容的类型: 从int转换到byte可能会有损失
byte d = 127 + 1; //wrong
```

这是一道很常见的面试题，其中错误的原因有两点：

   - 编译器可以识别常量，但是无法识别变量，常量可以在编译期间判断是否超出范围，但是两个变量相加，编译器在编译期间无法得知，所以会报错。
   - 编译器在编译期将该值作为int类型进行预编译计算后发现超出byte的取值范围，但是又是通过一个byte类型的变量去接收，所以就会出现可能会损失精度的异常。

这里很好的体现了整数类型的默认计算类型就是int类型~

### 浮点类型

浮点型有两种，一种是32位的`float`类型（单精度），一种是64位的`double`类型（双精度）。

| 名称 | 取值范围 |字节数|位数|包装类|
| --- | --- |---|---|---|
|float|大约$-3.4E+38$ 到 $+3.4E38$|8|32|Float|
|double|大约$-1.7E-308$ 到 $1.7E308$|16|64|Double|

因为`double`的取值范围更广，精度更高，所以我们日常都是使用`double`，默认的浮点类型也是`double`。

#### 关于float和long

从上面我们可以知道float是32位的，而long是64位的，下意识的我们会认为64位的取值范围必定要大于32位的，但事实并非如此：

float占了4个字节，也就是32位，其中第一位是符号位，23位是尾数位，剩下的8位都是指数位，$2^{8}$为256，由于（signed）符号数的原因，也就是说，float的取值范围大致位于$2^{-126}$到${2^{127}}$，是要远远的大于long的取值范围的。

其实，这也诠释了另外一个浮点数问题，因为计算机是二进制的，所以无法精确的表示出浮点数，但是Java也给我们了一种解决方案，那就是我们在涉及到浮点数比较敏感的地方（比如经纬度，金钱）的时候，一定要注意使用`BigDecimal`传参为**字符串**的方式！


>三个特殊的浮点数值：
>1. 正无穷大（Double.POSITIVE_INFINITY）
>2. 负无穷大（Double.NEGATIVE_INFINITY）
>3. NAN（Double.NaN）


### 字符型

`char`关键字所修饰的类型是字符型，需要由单引号引起来，一个或两个`char`类型的数值可以表示一个`Unicode`字符，我们所熟知的字符串底层数据结构正是一个字符数组常量：

```java
    /** The value is used for character storage. */
    private final char value[];
```
`char`类型其实是由`\u+十六进制数据的组成的`，最大值为`\uffff(65535)`，最小值为`\u0000(0)`。

这里需要注意一些特殊的转义字符：

| 转义序列 | 名称 | Unicode值 | 
| ------- |:-------:| :----:| 
| \b| 退格 | \u0008 | 
| \t| 制表 | \u0009 |
| \n| 换行 | \u000a | 
| \r| 回车 | \u000d |
| \\"| 双引号 | \u0022 |
| \\' | 单引号 | \u0027 |
| \\\ | 反斜杠 | \u005c |


### 布尔型

`boolean`修饰的变量就是布尔型，布尔类型很简单，只有`true false`两个值，但是这里需要注意，和**C++不同的地方是它不能由数字0或1转换成布尔型**。


### 强制类型转换

```java

byte a = 127; //right

byte b = 1; //right

byte c = a + b; // wrong

byte d = (byte)(a + b) // right

System.out.println(d);
```

还是这个熟悉的例子，刚刚我们已经分析了第三种情况为什么会报错，这里我们可以通过强制类型转换来强制完成这个操作。

> 强制类型转换只发生在**位数较多**的类型（int，64位）转为**位数较少**（byte，8位）的类型。

果不其然，我们将第三句注释掉之后，代码可以正常编译通过，然后我们去运行的时候，发现打印的d的值如下：

```
-128
```

这里就说到了强制类型转换会发生的一种情况，如果被转换的数值超出目标类型的取值范围，就会发生数据的丢失。

二进制在计算的时候，发生了超出数据范围的进位操作，随着强制类型转换，进位的部分被咔嚓掉，然后就发生这种情况了（熟悉原反补的同学应该明白这一点）。


### var

JDK 10中推出了一种新的类型`var`，猛地看起来很像`javascript`中的`var`，它可以这么玩：

```java
var list = new ArrayList<String>();
var x = 3;
```
乍一看，还真的和`javascript`有些像，但其实并不然，并不会影响Java是一个强类型语言的事实，它是基于局部变量推断机制来完成的，编译器在处理var时，先读构造器，并将它作为变量的类型，然后将该类型写入字节码当中。也就是说，该类型是无法更改的。

```js
var a = 3;
a = [1,2,3];
```
这样的写法在`javascript`中毫无问题，但是在Java中就不行。但是需要注意，`var`只能作用于带有构造器的**局部变量**和**for循环**中。



### 本篇重点总结

-  数据类型**四类八种**
-  float取值范围要大于long
-  强制转换只发生在**高位转低位**
-  **var**类型的原理是**局部类型推断**

