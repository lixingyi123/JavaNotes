<p align = "center" ><font size = 10， color = "#009999">Java-basic2</font></p>

[toc]

## Eclipse

### 简介

是一款辅助开发的开发工具，帮助我们对代码进行编译和执行，我们只需要关心文件的创建和编写

### 简单使用

```java
1.打开需要使用的窗口：
window-- 》show view
--》Project Explorer：打开项目目录，用于查看所有的项目以及Java文件
--》console：打开控制台

2.修改字体大小：
window-- 》preferences--搜索font

3.修改字符集
window-- 》preferences--搜索：workspace

4.创建项目：
filr--》new--》project

5.创建包：域名倒置，如net.wanhe

6.修改目录的展现形式：
点击目录栏右上角的三个点-->package presentation 

小结：
编译后的.class文件，存在工作空间（workspace）的bin目录中
真正运行的是bin中的代码
```

### 快捷键

1. 删除一行的程序：把光标放在要删除的那一行，使用：ctrl +D
2. 剪切：ctrl + X
3. 重新执行之前的命令：ctrl + Y
4. **Ctrl + /** ：自动补全代码和弹出窗口选择
5. **Alt+方向键上下**：上下行交换内容或把当前行内容把上或下移动
6. **ctrl+shift+/**：自动注释掉选择的代码块
7. **Ctrl+F11**： 再次运行上次启动的项目 

## 1、常量

### 1.0.1 常量的概念与分类

1. 常量的值不可以发生改变
2. 常量可以是整数，也可以是小数
3. 数学中的常数对应到Java中是常量，常数有分类，常量也有分类，且比数学中的分类更加丰富
4. 分类（6种）：
   - 整数常量：100
   - 小数常量：1.1，2.2
   - 字符常量：Java中规定用`''`引起来的只能写一个字符（不能不写，也不能写两个以上），
   - 字符串常量：用`""`引起来的可以写一个字符，也可以写多个字符
   - 布尔常量：只有true与false两个值
   - 空常量：null，注意：空常量不能直接打印

## 2、变量

### 2.0.1 变量的概念与分类

1. 变量的值可以改变
2. 变量用x, y, z等之类处理数据，数据是有类型的，把这种东西称为变量
3. 概念：在程序的执行过程中，其值可以在一定范围内改变。
4. 字符串不属于基本数据类型
5. 分类(1 Byte = 8 Bit)：
   - 整数型：byte（1字节，-2^7^~2^7^-1），short（2字节,大概是正负3万多），int（4字节，正负21亿，一般默认），long（8字节，大概19位数，后面加L）
   - 浮点型：float(4字节，后面加F/f)，double（8字节，默认）
   - 字符型：char（2字节,0~65535），可以存储任何字符，char 类型是一个==单一的== 16 位 Unicode 字符，字符的存储范围在`\u0000~\uFFFF`
   - 布尔型：boolean（1字节）

### 2.0.2 变量定义格式

1. 数据类型 变量名 = 数据值

2. 变量的本质就是内存中的一块空间，空间的大小由字符类型决定

3. ```java
   /*程序在内存（JVM）中运行，内存可以理解为田地，变量理解为萝卜坑
     1.一个萝卜一个坑
     2.大萝卜放大坑
     3.小萝卜放小坑
       
     Java中没有萝卜只有数据
     1.整数就放在整数坑中
     2.小数就放在小数坑中...
     先挖坑再种萝卜
       byte a;
       a = 10;
     * 先挖坑并给坑取一个名字，即先定义变量
     * 再种萝卜，将变量初始化
     * 可以修改坑里种的萝卜
   注意：大萝卜不能直接存在小坑中，小萝卜可以放到大坑中
   */
   ```


### 2.0.3 变量注意事项

1. 不能在同一个区域（同一个{}内）定义同名的变量
2. 变量必须初始化，也就是变量在使用前必须赋值
3. ==大萝卜（数据）不能直接存在小坑中，小萝卜可以放到大坑中==

## 3、标识符的含义与注意事项

1. 概念：程序中起名字的地方（类名，方法名称，变量名）
2. 命名规则：硬性要求
   - 标识符可以包含26个英文字母（区分大小写）、0-9、`_`下划线、`$`符号
   - 标识符不能以数字开头
   - 标识符不能是关键字

3. 命名规范(建议)：
   - 类名规范：首字母大写，后面每个单词首字母大写（大驼峰式）
   - 方法名规范：首字母小写，后面每个单词首字母大写（小驼峰式）
   - 变量名规范：首字母小写，后面每个单词首字母大写（小驼峰式）

4. 所有的**类都要放在包里**，==项目名和包名全部小写==
5. 取名时尽量可以**见名知意**

### 3.0.1 数据类型转换（理解）

1. **自动类型转换**

   ```java
   Java程序中要求参与计算的数据，必须保持数据类型一致性，如果数据类型不一致，将发生类型的转换
       int + int
       int + long ==> long + long (把int转换成long：从小到大，自动类型转换，不要代码干预)
       int + long ==> int + int  (把long类型转成int：从大到小，强制类型转换，必须手动代码完成)
   1.自动类型转换：取值范围小的数据或者变量可以直接赋值给范围大的变量
   2.特点：
       1.自动类型转换，不要代码干预
       2.byte/short/char 类型数据，只要参与运算会自动转换为int类型
       3.byte/short/char -->int -->long-->float -->double
   ```

   ```java
   package net.wanho.day02;
   
   public class Demo05Convert {
   	public static void main(String[] args) {
   		int i = 1;
   		byte b = 2;
   		/*
   		 * b是byte类型，i是int类型，运算时类型不一致，会发生类型的转换
   		 * byte类型（1个字节）的b会自动转换成int类型（4个字节）
   		 * 最终变成两个int类型的数据相加，结果是int（4个字节），不能直接赋值给
   		 * 左侧的byte类型的变量x的，占用1个字节
   		 */
   //		byte x = b + i;
   		int y = b + i;
   	}
   }
   ```

2. **强制类型转换**(可能造成精度缺失)

   ```java
   1.概念
       取值范围大的数据或者变量不能直接赋值给范围小的变量
       解决方案：
       	1.把坑变大
       	2.把萝卜变小（强制类型转换）
   2.格式
       转后类型 变量名称 = （转后类型）转前数据或者变量；
       long 类型（8个字节）的数字5
       long num = 5L;
   	long类型强制转换成int类型（4个字节）
       int a = (int)num;//把num中的数据强制转换成int类型，并把结果赋值给int变量a
   ```

   ```java
   package net.wanho.day02;
   
   public class Demo07Convert {
   	public static void main(String[] args) {
   		double d = 1.5;
   		int x = (int)d;
   		System.out.println(x);//1
   	}
   }
   ```

## ASCII码表

```java
计算机只认识0和1，所以存储到计算机中的所有内容都会转换成0和1进行存储
问题：如何把字符转换成0和1
通过ASCII码表：存储字符和数字对应关系的一张表
存储字符时：需要查找ASCII码表，找到对应的数字，将数字转换为二进制存放到计算机
    'A' ----->65 ----->1000001
    'a' ----->97------>1100001
使用字符时：将对应的二进制转换为十进制，找到ASCII码表中对应的字符
    1000001---->65---->'A'
    1100001---->97---->'a'
```

![](images\ASCII.png)

## 4、运算符（重要）

### 4.0.1 算术运算符

| 操作符 | 描述                                    | 例子       |
| ------ | --------------------------------------- | ---------- |
| +      | 加法-1.相加运算符两侧的值或2.字符串拼接 | A + B      |
| -      | 减法-左操作数减右操作数                 | A – B      |
| *      | 乘法-相乘操作符两侧的数                 | A * B      |
| /      | 除法-左操作数除以右操作数               | B / A      |
| %      | 取余-左操作数除以右操作数得到的余数     | B % A      |
| ++     | 自增-操作数的值增加1                    | B++ 或 ++B |
| --     | 自减-操作数的值减少1                    | B-- 或 --B |

```java
// + 运算符的特殊用法
package net.wanho.day02;

public class Demo11Operator {
	public static void main(String[] args) {
		/*
		 * +符号的作用
		 * 1.数学中的加法运算（数字相加）
		 * 2.字符串的拼接（把两个字符串连在一起）
		 */
		System.out.println(5+5);//10
		System.out.println("hello"+"World");//helloWorld
		System.out.println("*******************");
		//"5+5="+5+5 :从左向右计算
		//先计算"5+5="+5 ：此处+代表字符串的连接：5+5=5
		//然后"5+5=5"+5: 此处+代表字符串的连接："5+5=5"+55
		System.out.println("5+5="+5+5);//5+5=55
		//()的优先级比较高，所以先计算5+5
		System.out.println("5+5="+(5+5));//5+5=10
	}
}
```

### 4.0.2 自增自减运算符

```java
1.作用：让变量的值增加（++）或者减少（--）1
2.使用格式：
    1.写在变量前边： ++a、--a
    2.写在变量后边： a++、a--
3.使用特点：
    1.单独使用没有区别，都是让变量增加或者减少1
    2.混合使用：
    	前++/--: 先++/--再使用
        后++/--: 先使用，然后再++/--
```

**1、自增（++）自减（--）运算符**是一种特殊的算术运算符，在算术运算符中需要两个操作数来进行运算，而自增自减运算符是一个操作数。

实例

```java
public class selfAddMinus{
    public static void main(String[] args){
        int a = 3;//定义一个变量；
        int b = ++a;//自增运算
        int c = 3;
        int d = --c;//自减运算
        System.out.println("进行自增运算后的值等于"+b);
        System.out.println("进行自减运算后的值等于"+d);
    }
}
```

运行结果为：

```java
进行自增运算后的值等于4
进行自减运算后的值等于2
```

解析：

- int b = ++a; 拆分运算过程为: a=a+1=4; b=a=4, 最后结果为b=4,a=4
- int d = --c; 拆分运算过程为: c=c-1=2; d=c=2, 最后结果为d=2,c=2

**2、前缀自增自减法(++a,--a):** 先进行自增或者自减运算，再进行表达式运算。

**3、后缀自增自减法(a++,a--):** 先进行表达式运算，再进行自增或者自减运算 

实例

```java
public class selfAddMinus{
    public static void main(String[] args){
        int x = 4;
		int y = (x++) + (++x) + (x * 10);
		System.out.println("x = " + x); //6
		System.out.println("y = " + y); //4 + 6 + 60 = 70
    }
}
```

运行结果为：

```java
x = 6
y = 70
```

### 4.0.3 赋值运算符

分类：基本赋值运算符与复合赋值运算符

```java
1.如果复合运算符中运算结果的数据类型和左侧的数据类型不同，隐藏强制类型转换
2.整数常量只要不超出所赋值的整数变量的取值范围，可以直接赋值，内部隐藏强制类型转换
```

| 操作符 | 描述                                                         | 例子                                         |
| ------ | :----------------------------------------------------------- | -------------------------------------------- |
| =      | 简单的赋值运算符，将右操作数的值赋给左侧操作数               | C = A + B将把A + B得到的值赋给C              |
| +=     | 加和赋值操作符，它把左操作数和右操作数相加赋值给左操作数     | C + = A等价于C = C + A                       |
| -=     | 减和赋值操作符，它把左操作数和右操作数相减赋值给左操作数     | C - = A等价于C = C - A                       |
| *=     | 乘和赋值操作符，它把左操作数和右操作数相乘赋值给左操作数     | C * = A等价于C = C * A                       |
| /=     | 除和赋值操作符，它把左操作数和右操作数相除赋值给左操作数     | C / = A，C 与 A ==同类型==时等价于 C = C / A |
| %=     | 取模和赋值操作符，它把左操作数和右操作数取模后赋值给左操作数 | C％= A等价于C = C％A                         |

### 4.0.4 关系运算符

作用：比较数据之间的==大小关系==，一个`=`是赋值，两个`==`是判断比较两个操作数是否相同

**特点**：结果只能是true和false

| 运算符 | 描述                                                         |
| ------ | ------------------------------------------------------------ |
| ==     | 检查如果两个操作数的值是否相等，成立为true，不成立为false    |
| !=     | 检查如果两个操作数的值是否不相等，成立为true，不成立为false  |
| >      | 检查左操作数的值是否大于右操作数的值，成立为true，不成立为false |
| <      | 检查左操作数的值是否小于右操作数的值，成立为true，不成立为false |
| >=     | 检查左操作数的值是否大于或等于右操作数的值，成立为true，不成立为false |
| <=     | 检查左操作数的值是否小于或等于右操作数的值，成立为true，不成立为false |

### 4.0.5 逻辑运算符

作用：用来连接多个条件，最终结果是布尔类型

```java
1.&& 与 & 区别：&& 中如果 a 为 false，则不计算 b（因为不论 b 为何值，结果都为 false）
2.|| 与 | 区别：|| 中如果 a 为 true，则不计算 b（因为不论 b 为何值，结果都为 true）
3.&&和||能够采用最优化的计算方式，从而提高效率。在实际编程时，应该优先考虑使用短路与和短路或。
```

| 运算符 | 用法   | 含义     | 说明                                               |
| :----: | :----- | :------- | :------------------------------------------------- |
|   &&   | a&&b   | 短路与   | ab 全为 true 时，计算结果为 true，否则为false。    |
|  \|\|  | a\|\|b | 短路或   | ab 全为 false 时，计算结果为 false，否则为 true。  |
|   !    | ! a    | 逻辑非   | a 为 true 时，值为 false，a 为 false 时，值为 true |
|   \|   | a \| b | 逻辑或   | ab 全为 false 时，计算结果为 false，否则为 true    |
|   &    | a & b  | 逻辑与   | ab 全为 true 时，计算结果为 true，否则为 false     |
|   ^    | a ^ b  | 逻辑异或 | ab 全为 true 时，计算结果为 false，否则为true      |

### 4.0.6 三元运算符

1. 格式

   数据类型 变量名称 = 布尔表达式1 ？表达式2 ：表达式3；

2. 执行流程

   - 计算布尔表达式1的结果，true或false
   - 如果结果为true，就把表达式2的结果赋值给左侧的变量
   - 如果结果为false，就把表达式3的结果赋值给左侧的变量

```java
package net.wanhe.day03;
/*练习：一座寺庙里住着三个和尚，已知三个和尚的身高分别为：150cm，210cm，165cm
用程序获取这三个和尚的最高身高*/
public class Test {
	public static void main(String[] args) {
		int h1 = 150, h2 = 210, h3 = 165;
		int mid = h1 > h2 ? h1 : h2;
		System.out.println("三个和尚的最高身高为:" + (mid > h3 ? mid : h3) + "cm");	
	}
}
```

## 5、数据输入

### 5.0.1 键盘输入的基本使用

数据输出：把程序的结果输出到控制台，显示到屏幕上

数据输入：获取用户从键盘录入的数据到程序中

#### 1:导包--建对象--使用

```java
jdk中把获取键盘录入数据的功能放到了java.util包的Scanner类中
键盘录入的使用：
   固定的三个步骤：
   1：导包（找到需要使用的功能，告诉java我们需要使用的功能在哪）
	  格式：
	  import  包名.类名
	  import  java.util.Scanner
    
   2：创建对象
	  格式：
      类名 对象名 = new 类名(...);
	  类名：就是之前写代码时class关键字后面的名字
      Scanner sc = new Scanner(System.in); // 固定写法

   3：使用（使用next()系列的方法接收数据）
      sc.nextXxx(); // 获取键盘录入的整数或小数数字
	  sc.next()/sc.nextLine(); // 获取从键盘录入的字符串
      sc.hasNextXxx(); // 使用hasNextXxx()方法进行验证，再使用nextXxx()来读取

   4：next()与nextLine()方法之间的区别
      next():
		1、一定要读取到有效字符后才可以结束输入。
		2、对输入有效字符之前遇到的空白，next()方法会自动将其去掉。
		3、只有输入有效字符后才将其后面输入的空白作为分隔符或者结束符。
		4、next() 不能得到带有空格的字符串。
	  nextLine()：
		1、以Enter为结束符,也就是说nextLine()方法返回的是输入回车之前的所有字符。
		2、可以获得空白。
            
   5：说明（注意）
       1、当输入多个数据时，第一个next()接收到数据，下一个next()发现字节流里面有东西，就不会阻塞等待输入了，会直接接收。例如：输入“This is Java code” ，用next()只接受一个单词“This”，下面用nextLine()接收了其他剩余的部分
       2、要输入 int 或 float /double类型的数据，最好先使用 hasNextXxx() 方法进行验证。
       3、Scanner对象用完最后用close()关闭掉，不然会告警。
```

```java
package net.wanhe.day03;
import java.util.Scanner;

// 练习：获取键盘录入的两个整数数字，在控制台输出求和结果
// 快捷键，ctrl + 1 + 回车，自动补全代码
public class ScannerText {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		
		System.out.print("请输入第一个整数数字num1:");
		int num1 = sc.nextInt();
		System.out.print("请输入第二个整数数字num2:");
		int num2 = sc.nextInt();
		
		System.out.println(num1 + " + " + num2 + " = " + (num1 + num2));
		sc.close();
	}
}
```

```java
package net.wanhe.day03;
import java.util.Scanner;

// next()与nextLine()的区别练习
public class DemoIf {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		
		System.out.print("请输入第一串字符串：");
		String str_next = sc.next();
		System.out.println(str_next);
		
		//System.out.print("请输入第二串字符串：");
		//String str_nextline = sc.nextLine();
		//System.out.println(str_nextline);
		sc.close();
	}
}

结果：
请输入第一串字符串： ert ffg
ert
请输入第二串字符串： tyu uuiu
 tyu uuiu
```

## 6、流程控制

流程是人们生活中不可或缺的一部分，它表示人们每天都按照一定的流程做事。程序设计也需要有流程控制语句来完成用户的要求，根据用户的输入决定程序要进入什么流程，即“做什么”和“怎么做”等。

### 6.0.1 流程控制的分类

```java
分类：
	1.顺序结构，从上到下依次执行
	2.选择/分支结构
	  if语句（重要）
	  switch语句
	3.循环结构
	  for循环
	  while循环
	  do-while循环
```

### 6.1：选择语句—if

#### 6.1.1：选择语句-if

```java
if：结果
1.if语句语法格式：
    if(布尔表达式){
    	语句体1;
    }
    其他代码
2.执行步骤：
   1）先计算if后面的布尔表达式的结果
   2）根据结果进行判断，如果结果是true，就执行if后面{}中的语句体1，接着执行其他代码
   3）如果结果是false，跳过if后面的{}中的语句体，接着执行其他代码
```

#### 6.1.2：选择结构--if-else

```java
if：结果， else（可有可无，按照需求增加）：其他，否则
1.if语句语法格式：
    if(表达式){
    	语句体1;
    }else{
    	语句体2;
    }
    其他代码
2.执行步骤：
   1）先计算if后面的布尔表达式的结果
   2）根据结果进行判断，如果结果是true，就执行if后面{}中的语句体1，接着执行其他代码
   3）如果结果是false，跳过if后面的{}中的语句体，执行else里面的语句体2，接着执行其他代码
```

```java
package net.wanhe.day03;
// 导包
import java.util.Scanner;

// 练习需求：任意给出一个整数，判断该整数是奇数还是偶数，并在控制台输出

public class DemoIf {
	public static void main(String[] args) {
        // 建立对象
		Scanner sc = new Scanner(System.in);
		System.out.print("请输入一个整数：");
		int num = sc.nextInt();
		if(num % 2 == 0) {
			System.out.println(num + "是一个偶数");
		}else {
			System.out.println(num + "是一个奇数");
		}
		sc.close();
	}
}
```

![](images\if-else.png)

#### 6.1.3：选择结构-if-else if -else

```java
if：结果， else（可有可无，按照需求增加）：其他，否则
1.if语句语法格式：
    if(表达式1){
    	语句体1;
    }else if(表达式2){
    	语句体2;
    }...else if(表达式n){
    	语句体n;
	}else{
		语句体n+1;
	}
    其他代码
2.执行步骤：
   1）先计算if后面的表达式1的
   2）根据结果进行判断，如果结果是true，就执行if后面{}中的语句体1。否则就接着执行表达式2，结果为true，则执行语句体2...
   3）如果没有表达式的结果为true，就执行语句体n+1
```

![](images\if-else-if.jpg)

### 6.2：选择语句—switch

```java
格式：
 switch(表达式){
 	case 常量值1:
 		语句体1;
 		break;
 	case 常量值2:
 		语句体2;
 		break;
 	...
 	case 常量值n:
 		语句体n;
 		break;
 	default:
 		语句体n+1;
 		break;
 }
 其他语句;
 
 执行流程：
 	1.首先，计算表达式的值
 	2.其次，和case依次比较，一旦有对应的值，就执行相应的语句，在执行的过程中，遇到break就结束switch语句
 	3.最后，如果所有的case和表达式都不匹配，就会执行default语句，然后结束流程
```

注意事项：

1. break的作用是结束switch语句的，一旦执行break，直接跳出switch到switch外面执行其他语句
2. switch()后面的表达式数据类型：
   - 基本类型：byte/short/int/char
   - 引用类型：String或者枚举

3. case后面的值不能重复
4. 最后的default是用来兜底的
5. 如果default放在最后，后面的break可以省略
6. 如果所有的case和default后面都有break，那么default和case顺序可以任意
7. 在switch中，如果case后面不写break，将出现穿透现象，也就是不会再判断下一个case的值，直接向后运行，直到遇到break，或者整体switch结束

```java
package net.wanhe.day03;
import java.util.Scanner;

public class DemoSwitch {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		System.out.print("请输入月份(1-12):");
		int month = sc.nextInt();
		switch(month){
			case 3:
            case 4:
            case 5:
				System.out.println("春天");
				break;
			case 6:
            case 7:
            case 8:
				System.out.println("夏天");
				break;
			case 9:
            case 10:
            case 11:
				System.out.println("秋天");
				break;
			case 12:
            case 1:
            case 2:
				System.out.println("冬天");
				break;
			default:
				System.out.println("输入的数据有误");
		}
		sc.close();
	}
}
```

switch语句练习：

```java
package net.wanhe.day03;
import java.util.Scanner;

public class Text2 {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		System.out.print("请输入第一个整数：");
		int num1 = sc.nextInt();
		System.out.print("请输入第二个整数：");
		int num2 = sc.nextInt();
		System.out.println("------xxx的计算器-------");
		System.out.println("1.求和");
		System.out.println("2.求差");
		System.out.println("3.求商(取整)");
		System.out.println("4.求积");
		System.out.print("请选择：");
		int select = sc.nextInt();
		switch(select) {
		case 1:
			System.out.println(num1 + " + " + num2 + " = " + (num1 + num2));
			break;
		case 2:
			System.out.println(num1 + " - " + num2 + " = " + (num1 - num2));
			break;
		case 3:
			System.out.println(num1 + " / " + num2 + " = " + (num1 / num2));
			break;
		case 4:
			System.out.println(num1 + " * " + num2 + " = " + (num1 * num2));
			break;
		default:
			System.out.println("输入的数据有误");
		}
		sc.close();
	}
}
```

### 6.3：循环结构

#### 6.3.1：循环-for（重要）

概述：重复性的执行某些固定的操作，当条件不成立时，结束循环，条件成立时，继续执行操作

```java
1.for循环格式
    for(初始化表达式1;布尔表达式2;步进表达式4){
        循环体3;
    }

2.执行流程：
    初始化表达式1-->布尔表达式2-->循环体3-->步进表达式4——》布尔表达式2-->循环体3-->步进表达式4...直到布尔表达式2为false就结束循环，开始执行循环后面的其他语句
    
3.循环的分类
    for
    while
    do-while
```

for循环练习：键盘上输入一个三位数，判断是不是水仙花数，水仙花数是指一个三位数的个位，十位，百位的数字立方和等于原数

```java
import java.util.Scanner;

// 键盘上输入一个三位数，判断是不是水仙花数，是指一个三位数中，个位，十位，百位的数字立方和等于原数
public class Text5 {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		System.out.println("请输入一个三位数：");
		int num = sc.nextInt();
		int temp1 = num;
		int temp = num;
		int sum = 0;
		for(int i = 3; i > 0; i--) {
			temp = num % 10;
			sum += temp * temp * temp;
			num /= 10;
		}
		if(sum == temp1) {
			System.out.println(temp1 + "是一个水仙花数");
		}else {
			System.out.println(temp1 + "不是一个水仙花数");
		}
		sc.close();
	}
}
```

#### 6.3.2：循环-while

```java
1.格式
    初始化表达式1;
    while(布尔表示式2){
        循环体3;
        步进表达式4; // 容易被遗忘造成死循环
    }
	其他语句;

2.步骤：
    初始化表达式1-->布尔表示式2-->循环体3-->步进表达式4--》布尔表示式2-->循环体3-->步进表达式4-->...-->直到布尔表达式的结果为false，就退出循环
```

#### 6.3.3：循环-do-while（不常用）

1. do···while循环语句与while循环语句的区别是，while循环语句先判断条件是否成立再执行循环体，而do···while循环语句则先执行一次循环后，再判断条件是否成立。也即==do···while至少执行一次==。

```java
1.格式
	do{
	  执行语句1;
	} while (条件表达式2);

2.执行流程：
    1，2-->1，2--直到表达式为false结束循环
```

```java
// while与do...while进行比较
int a = 10;
int b = 10;

while (a == 8){
	System.out.println("a = " + a);
	a--;
}

do{
	System.out.println("b = " + b);
	b--;
} while(b == 8);

结果为b = 10
    while循环语句中，进入while的语句块的条件是a == 8，很明显不成立，所以不执行，结果中没有关于a的结果。然后再看do···while循环语句，先执行一次do后的语句块，输出“b == 10”，然后判断while条件b == 8不成立，循环结束，所以结果只有一个do···while语句中执行的第一步b = 10。
```

#### 6.3.4：循环语句的使用

>1、循环次数确定，建议使用for循环，循环次数不确定使用while
>
>2、while与do-while中初始化的变量接下来可以继续使用，而for循环中的初始化变量离开循环后不能再使用
>
>3、do-while循环至少执行一次

#### 6.3.5：循环嵌套

```java
1.格式
    外层循环执行一次，内层循环执行完整的一遍
    for (初始化表达式1; 布尔表达式2; 步进表达式7){  // 外层循环
        for (初始化表达式3; 布尔表达式4; 步进表达式6){ // 内层循环
            循环体5;
        }
    }

2.执行流程：
    初始化表达式1，布尔表达式2，初始化表达式3，布尔表达式4，循环体5，步进表达式6--》布尔表达式4，循环体5--》..--》直到内层循环的布尔表达式4为false，结束内层循环--》步进表达式7，布尔表达式2，...-->直到布尔表达式2为false，结束全部循环
```

```java
// 循环嵌套练习
// 使用循环嵌套模拟时钟
// 时针走一格，分针走一圈
public class HourText{
    public static void main(String[] args){
        for (int hour = 0; hour < 24; hour++){
            for (int minute = 0; minute < 60; minute++){
                System.out.println(hour + "点" + minute + "分");
            }
        }
    }
}
```

### 6.4：跳转语句

#### 6.4.1：语句break

1. break语句在switch中已经见过了，是用来中止case的。实际上break语句在for、while、do···while循环语句中，用于==强行退出当前循环==，为什么说是当前循环呢，因为**break只能跳出离它最近的那个循环的循环体**，假设有两个循环嵌套使用，break用在内层循环下，则**break只能跳出内层循环**
2. 可以利用 boolean flag对循环进行标记，跳出多层循环 

```java
public static void main(String[] args){
	System.out.println("早上买了4个包子，开始吃了");
	for (int i = 1; i < 5; i++){
		if (i == 3){
			System.out.println("第三个包子上有小强，不吃了，没胃口了");
			break;
		}
    	System.out.println("正在吃第" + i + "个包子");
	}
}
结果：
早上买了4个包子，开始吃了
正在吃第1个包子
正在吃第2个包子
第三个包子上有小强，不吃了，没胃口了
```

#### 6.4.2：语句continue

continue语句只能用于for、while、do···while循环语句中，用于让程序直接跳过其后面的语句，**进行下一次循环**。

```java
public static void main(String[] args){
	System.out.println("早上买了4个包子，开始吃了");
	for (int i = 1; i < 5; i++){
		if (i == 3){
			System.out.println("第三个包子掉地上了，不能吃了");
			continue;
		}
    	System.out.println("正在吃第" + i + "个包子");
	}
}

结果：
早上买了4个包子，开始吃了
正在吃第1个包子
正在吃第2个包子
第三个包子掉地上了，不能吃了
```

#### 6.4.3：语句return

1. return语句可以用来结束一个方法，当一个方法执行到return语句时，这个方法将被结束。

2. return语句可以从一个方法返回，并把控制权交给调用它的语句
3. return语句直接结束掉整个方法，不管这个return处于多少层循环之内

```java
public void getName() {
    return name;
}
// 这是一个方法用于获取姓名，当调用这个方法时将返回姓名值。
```

## 7、随机数

### 7.1：Random()

>1.Random类就是产生随机数，也是一种引用数据类型
>
>2.使用步骤：
>
>​	1：导入：java.util.Random;
>
>​	2：建对象：Random r = new Random();
>
>​	3：使用nextXxx()
>
>​		int num = r.nextInt(); // 随机产生一个int范围类的随机数
>
>​		int num = r.nextInt(整数数字n)；// 产生数字之内[0-n）的随机数
>
>​		int num = r.nextInt()
>
>​	4：**公式：（max – min）+ 1）+ min**
>
>​		上面的公式将在min（含）和max（含）之间生成一个随机整数。

```java
Random r = new Random();
System.out.println("10个int范围类的随机整数数字为：");
for (int i = 0; i < 10;i++) {
	int num = r.nextInt();
	System.out.print(num + " ");
}
		
System.out.println();
System.out.println();
System.out.println("10个[0,100)范围类的随机整数数字为：");
for (int i = 0; i < 10;i++) {
	int num = r.nextInt(100);
	System.out.print(num + " ");
}
		
System.out.println();
System.out.println();
System.out.println("2个[1,5]范围类的随机整数数字为：");
for (int i = 0; i < 2;i++) {
	int num = r.nextInt((5 - 1) + 1) + 1;
	System.out.print(num + " ");
}
		
System.out.println();
System.out.println();
System.out.println("10个[1,100]范围类的随机整数数字为：");
for (int i = 0; i < 10;i++) {
	int num = r.nextInt((100 - 1) + 1) + 1;
	System.out.print(num + " ");
}
		
System.out.println();
System.out.println();
System.out.println("10个[66,178]范围类的随机整数数字为：");
for (int i = 0; i < 10;i++) {
	int num = r.nextInt((178 - 66) + 1) + 66;
	System.out.print(num + " ");
}
```

### 7.2：随机数练习（猜数字游戏）

需求：随机生成一个0-100之间的数字，键盘录入去猜生成的数字是多少

```java
import java.util.Random;
import java.util.Scanner;

// 需求：随机生成一个0-100之间的数字，键盘录入去猜生成的数组是多少
public class GuessNumGame {
	public static void main(String[] args) {
		// 随机生成一个数字
		Random r = new Random();
		int random = r.nextInt(101);
		// 猜数字
		Scanner sc = new Scanner(System.in);
		int count = 0;
		System.out.println("我心中有一个0到100之间的数字，你猜猜是什么？");
		do {
			int guess = sc.nextInt();
			if(guess > random) {
				System.out.println("大了点，再猜!");
				count++;
			}else if(guess < random) {
				System.out.println("小了点，再猜!");
				count++;
			}else {
				System.out.println("恭喜你，猜对了，就是" + guess);
				count++;
				break;
			}
		} while(true);
		System.out.println("你猜的次数是：" + count + "次");
		// 评价
		if(count < 5) {
			System.out.println("你太厉害了,很快就猜对了");
		}else if(count >= 5 && count <= 10) {
			System.out.println("不错不错！");
		}else {
			System.out.println("加油！！");
		}
		sc.close();
	}
}
```

