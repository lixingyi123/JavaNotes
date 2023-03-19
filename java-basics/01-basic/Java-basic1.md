<p align = "center" ><font size = 10， color = "#009999">Java-basic1</font></p>

[toc]

## 1、Java基础概述

### 1.1 Java语言概述

1. Java是一种高级编程语言，而且是面向对象的编程语言。
2. Java语言是美国Sun公司（Stanford University Network），在1995年推出的高级的编程语言
3. Java语言共同创始人之一：詹姆斯·高斯林 （James Gosling），被称为“Java之父”
4. Java语言的版本：1.0-1.4，5.0...8.0...13.0...

### 1.2 Java语言能做什么

Java语言主要应用在互联网程序的开发领域
网上购物商城
物流
金融
各行各业的网站

### 1.3 Java语言的跨平台实现原理

```java
JVM: Java虚拟机,是专门用来运行Java程序的
平台: 指的就是操作系统,比如windows,linux,macos等
跨平台: 我们编写的一个Java程序,可以做多个操作系统上运行
		一次编译,到处运行
    
1.问题1
	Java程序是跨平台的?	正确的
		一次编译到处运行

2.问题2
	JVM是跨平台的? 错误的
	JVM是实现Java程序跨平台的基石
	针对不同的操作系统提供不同的JVM
	而程序在JVM中运行

3.问题3
	Java程序的跨平台是依靠JVM实现的
	正确的
```

### 1.4 JDK--JRE--JVM

```
JDK：是Java Development Kit的缩写，是Java的开发工具包。JDK是整个JAVA的核心，包括了Java运行环境（JRE），Java工具（javac/java/jdb等）和Java基础的类库（即Java API ）。

JRE：（Java Runtime Environment，Java运行环境）是Java运行环境，并不是一个开发环境，所以没有包含任何开发工具（如编译器和调试器），只是针对于使用Java程序的用户。包含JVM标准实现及Java核心类库。

JVM：(Java Virtual Mechinal)，Java虚拟机，是JRE的一部分。它是整个java实现跨平台的最核心的部分，负责解释执行字节码文件，是可运行java字节码文件的虚拟计算机。

三者关系： JDK 包含 JRE 包含 JVM
```

## 2、Java环境搭建

JDK下载:https://www.oracle.com/

安装教程：[jdk8的安装和环境配置](https://zhuanlan.zhihu.com/p/147985069)

## 3、Hello World入门程序

### 3.1 程序开发的步骤

```java
1.源程序（HelloWorld.java）:
	程序员写的程序
	程序的组成: 字母,数字,其他符号
	本质就是一个文本文件,但是扩展名不是.txt,而是.java
    
2.生产JVM可以执行的字节码(.class)文件
    JVM: 叫做Java虚拟机,是专门用来运行Java程序的
    但是JVM只能识别0和1,而存储0和1的文件叫做字节码文件(.class文件)
    如何把源文件(程序)翻译成JVM能够执行的字节码文件(程序)呢?
    使用javac命令(编译命令)
    使用格式: javac 文件名.java
    编译HelloWorld.java源文件: javac HelloWorld.java
    生成一个字节码文件: HelloWorld.class 
        
3.把字节码文件交给JVM执行
	不会自动执行,如何把字节码文件交给JVM执行呢?
    使用java命令(运行命令)
	使用格式: java 文件名
	java HelloWorld
```

### 3.2 Hello World案例的编写编译运行

```java
1.编写源文件
    创建一个名称为HelloWorld.txt的文本文件,把扩展名修改为.java
    打开HelloWorld.java源文件,输入以下内容,并保存(ctrl+s)
    public class HelloWorld {
        public static void main(String[] args){
            System.out.println("HelloWorld");
        }
    }

2.编译: javac命令
    根据.java源文件生产对应的.class文件(字节码文件)
    使用javac命令的格式:
		javac 文件名.java
        javac HelloWorld.java
            
            
3.运行: java命令            
    把字节码(.class)文件交给jvm执行
    使用java命令的格式:
		java 文件名
        java HelloWorld 
```

## 4、进制

### 4.1 分类

二进制：只有0与1

八进制：每位数字0-7，逢8进1

十进制：平常生活中使用的进制，0-9

十六进制：数字0-9，10：A/a    11:B/b    12:C/c    13:D/d   14:E/e    15:F/f

### 4.2 转换

#### 4.2.1 二进制转十进制

二进制的每一位（从右向左）第一位是2的0次方，第二位是2的1次方，以此内推

例如：1101（2）= 13

#### 4.2.2 十进制转二进制

数字除以2取余数，倒过来返回写就是二进制

![](images\十转二.png)

