---
layout: post
title:  Java 极客技术建议写作规范
tagline: by 纯洁的微笑
categories: 写作规范
tags: 
    - 纯洁的微笑
---

本文由纯洁的微笑所起草，欢迎团队内成员在此基础上维护、完善。

<!--more-->


## 博客文件规范

- 1、文章命名为： 日期+英文标题，标题英文中间用中杠连接，例如：2019-02-25-java-history.md
- 2、在文中的第一段下面添加`<!--more-->`表示，作为文章在首页的预览内容。
- 3、文中图片上传到`/assets/images/2019/`目录地址下，可以根据情况新建目录。
- 4、文章内容由 Markdown 书写。


## 文章内容规范

- 1、文章中英文之间需要留有空格。     
- 2、每篇文件，建议由开头场景解释，结尾有总结，最好多使用图片讲解。  
- 3、文章中图片推荐写全地址，比如 `![](http://www.justdojava.com/assets/images/2019/java/James_Gosling_2008.jpg) `  
- 4、`#` 为一级标题、 `##` 为二级标题、`##`三级标题 ，不建议文章目录大于三级，标题上下需要留空行，可以直接从二级标题开始。  
- 5、代码写作规范；如果是单行代码片段建议使用：`代码片段`格式；如果是多行代码建议使用以下方式：  

```
多行其它代码
```

``` java
多行 Java 代码
```

代码建议紧贴左侧不要留有空格。多行代码和上下文之间需要留有空行。


## 其它

待补充...


## Markdown 介绍
Markdown 是一种轻量级标记语言，创始人为约翰·格鲁伯（John Gruber）。它允许人们“使用易读易写的纯文本格式编写文档，然后转换成有效的XHTML(或者HTML)文档”。这种语言吸收了很多在电子邮件中已有的纯文本标记的特性。

## 常用语法

### 标题

``` xml
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题
```

注：# 和「一级标题」之间建议保留一个字符的空格，这是最标准的 Markdown 写法。

### 列表

列表格式也很常用，在 Markdown 中，你只需要在文字前面加上 - 就可以了，例如：

``` xml
- 文本1
- 文本2
- 文本3
```

如果你希望有序列表，也可以在文字前面加上 1. 2. 3. 就可以了，例如：

```  xml
1. 文本1
2. 文本2
3. 文本3
```

注：-、1.和文本之间要保留一个字符的空格。

### 链接和图片

在 Markdown 中，插入链接不需要其他按钮，你只需要使用 `xml[显示文本](链接地址)` 这样的语法即可，例如：

```  xml
[Deadpool](http://img31.mtime.cn/mg/2016/02/05/145836.38850143_210X210X4.jpg)
```

在 Markdown 中，插入图片不需要其他按钮，你只需要使用`![](图片链接地址)`这样的语法即可，例如：

``` xml
![](http://img31.mtime.cn/mg/2016/02/05/145836.38850143_210X210X4.jpg)
```

注：插入图片的语法和链接的语法很像，只是前面多了一个 ！。

效果如下：<br />
[Deadpool](http://img31.mtime.cn/mg/2016/02/05/145836.38850143_210X210X4.jpg)<br />
![](http://img31.mtime.cn/mg/2016/02/05/145836.38850143_210X210X4.jpg)

### 引用

在我们写作的时候经常需要引用他人的文字，这个时候引用这个格式就很有必要了，在 Markdown 中，你只需要在你希望引用的文字前面加上`>`就好了，例如：

> markdown 引用

注：> 和文本之间要保留一个字符的空格。

###  粗体和斜体

Markdown 的粗体和斜体也非常简单，用两个`*`  包含一段文本就是粗体的语法，用一个 `*`包含一段文本就是斜体的语法。例如：

```  xml
 *一盏灯*， 一片昏黄；**一简书**， 一杯淡茶。 守着那一份淡定， 品读属于自己的寂寞。 保持淡定， 才能欣赏到最美丽
```

最终显示的就是下文，其中「一盏灯」是斜体，「一简书」是粗体：

### 表格

相关代码：

```  xml
| Tables        | Are           | Cool  |
| ------------- |:-------------:| -----:|
| col 3 is      | right-aligned | $1600 |
| col 2 is      | centered      |   $12 |
| zebra stripes | are neat      |    $1 |
```

显示效果：


| Tables        | Are           | Cool  |
| ------------- |:-------------:| -----:|
| col 3 is      | right-aligned | $1600 |
| col 2 is      | centered      |   $12 |
| zebra stripes | are neat      |    $1 |


### 代码高亮

```  xml
使用``` xxx 开头 ，```结尾的代码块； xxx 代表了语言，比如：Java、xml、js等；

示例：

*``` java
this is java code space
*```
```

效果如下：

``` java
this is java code space
```