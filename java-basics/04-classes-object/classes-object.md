<p align = "center" ><font size = 10， color = "# 009999">Classes & Objects</font></p>

## 1、面向过程和面向对象编程思想

编程思想其实就是编程思路，开发中常用的就是面向过程编程思想和面向对象编程思想。

1. **面向过程编程思想**：强调过程，必须弄清楚每一个步骤，然后按照步骤一步一步实现

2. **面向对象编程思想**：通过调用对象的行为（方法）来实现功能，而不是一步一步去实现

   例子：面向对象：洗衣服：把衣服脱下来--》交给女朋友洗

   ​			面向过程：洗衣服：脱衣服--》放盆里--》放洗衣机--》放洗衣液--》取衣服--》晾衣服

## 2、类的概述

概念：**类就是描述一类具有共同属性和行为事物的统称**，抽象的，只是用来描述数据信息的

#### 2.1 类的组成

属性（状态）（实例变量[instance variable]）：就是该事物本身已知的事物

行为（方法）：就是该事物能够执行的动作

比如：人

​	属性：姓名，性别，年龄，身高...

​	行为：吃饭，睡觉，学习，做饭...

## 3、对象的概述

概念：**对象是类的一个实例，具体存在，具备类的一切属性和行为**

对象的属性：对象的属性有特定的值

对象的行为：对象可以操作的行为

## 4、类和对象的关系

类是用来描述一类具有共同属性和行为事物的统称

对象是一类事物的具体实例

类是对象的蓝图，对象是类的实体

## 5、类的定义

实例变量：该类事物的状态信息，在类中通过成员变量体现

行为：该类事物有什么功能，在类中通过成员方法来体现

### 5.1 类的定义步骤

1. 定义类
2. 编写类的成员变量
3. 编写类的成员方法

```java
public class 类名{ // 定义一个类
    // 实例变量
    数据类型 变量名1;
    数据类型 变量名2;
    ...
    
    // 行为（方法），没有static修饰符
    ...
}
```

```java
// phone类
public class Phone {
	// 实例变量
	
	int price; // 价格
	String color; // 颜色
	String brand; // 品牌
	
	
	// 方法
	public void call(String phoneNum) {
		System.out.println("正在给" + phoneNum + "打电话...");
	}
	
	public void sendMassage(String phoneNum, String massage) {
		System.out.println("正在给" + phoneNum + "发送信息" + massage);
	}
}
```

![](images\类的定义.png)

### 5.2 对象的创建

#### 5.2.1 前提

创建一个对象，需要两个类，一个是被操作与对象的类，例如Phone类，另一个是测试该类的类

测试类一般被命名为==受测类名称 + TestDrive==，并使用圆点运算符来存取该对象的属性和方法。

#### 5.2.2 创建对象的格式

==类名 对象名 = new  类名();==

例如：Phone phone = new Phone();

### 5.3 对象的使用

#### 5.3.1 调用成员变量的格式

使用**圆点运算符**来存取该对象的属性和方法。

```java
访问成员变量：

​	获取成员变量的值：对象名.成员变量名；

​	给成员变量赋值：对象名.成员变量名 = 值；

访问成员变量方法：

​	对象名.成员方法();
```



```java
// Phone的测试类

public class PhoneTestDrive {
	public static void main(String[] args) {
		// 创建phone类的对象
		Phone phone = new Phone();
		
		// 给成员变量赋值
		phone.brand = "华为";
		phone.color = "粉色";
		phone.price = 4567;
        
		// 获取并输出成员变量的信息
        System.out.println(phone.brand);
		System.out.println(phone.color);
        System.out.println(phone.price);
		
		// 使用phone对象调用call方法
		phone.call("143xxxxxxxx");
        // 使用phone对象调用sendMessage方法
		phone.sendMassage("143xxxxxxxx", "你好呀！！");
	}
}
```

### 5.4 类和对象的练习

需求：创建一个Student类，定义几个成员变量，写几个功能方法（学习，睡觉，吃饭，上课，玩手机，打游戏...）

```java
// Student类
public class Student {
	// 成员变量
	String name;
	int age;
	String grade;
	
	// 方法
	public void study(String name){
		System.out.println(name + "正在学习中，请勿打扰...");
	}
	
	public void lessons(String name, String lesson) {
		System.out.println(name + "正在教学楼上" + lesson + "课");
	}
}

// Student测试类
public class StudentTestDrive {
	public static void main(String[] args) {
		// 创建对象
		Student student = new Student();
		
		// 给对象赋值
		student.name = "xxx";
		student.age = 21;
		student.grade = "四年级";
		
		
		// 输出信息
		System.out.println(student.name);
		System.out.println(student.age);
		System.out.println(student.grade);
		
		// 方法
		student.study("xxx");
		student.lessons("xxx", "英语");
	}

}

```

### 5.5 成员变量默认值

```java
public class StudentTestDrive {
	public static void main(String[] args) {
		// 创建对象
		Student student = new Student();
		
		System.out.println(student.name);
		System.out.println(student.age);
		System.out.println(student.grade);
	}

}

结果：
null
0
null
```

## 6、单个对象创建在内存中的图解（重要）

### 6.1 记忆（重要）

Java程序内存：栈内存，堆方法，方法区

1. jvm首先会**调用main方法**执行整个程序（入口）

2. Java程序第一次使用某个类，就会把该类的字节码文件（class文件）加载到方法区中
3. 凡是new就会在堆中开辟一块空间
4. 方法一旦调用就会被加载到栈区，开辟一块新的空间来执行方法
5. 方法执行完毕后，就会弹栈（回收方法执行占用的空间）
6. 对象是根据类来创建的，类有什么对象就有什么

![](images\一个对象的创建的内存图.png)

## 7、成员变量和局部变量的区别

1. **类中的位置不同**：成员变量在类中方法外，局部变量在方法内部或者方法声明上
2. **在内存中的位置不同**，成员变量在堆内存中，局部变量在栈中
3. **生命周期不同**，成员变量随着**对象**的存在而存在，随着对象的消失而消失，局部变量随着**方法**的调用而存在，方法的调用完毕而消失
4. **初始值不同**，成员变量有默认初始值，局部变量没有默认初始值，在使用前必须先初始化

## 8、封装

### 8.1 封装概述

封装是面向对象三大特征之一（封装，继承，多态）

封装原则：将类的某些信息隐藏在类内部，不允许外部程序直接访问，而是通过该类提供的方法（setXxx()或者getXxxx()）来实现对隐藏信息的操作和访问被private修饰的成员变量

### 8.2 private关键字的使用

#### 8.2.1 安全隐患

原因：通过对象名直接访问成员变量，会存在安全隐患

```java
// Student类
public class Student {
	// 成员变量
	String name;
	int age;
	String grade;
	
	// 方法
	public void study(String name){
		System.out.println(name + "正在学习中，请勿打扰...");
	}
	
	public void lessons(String name, String lesson) {
		System.out.println(name + "正在教学楼上" + lesson + "课");
	}
}

// Student测试类
public class StudentTestDrive {
	public static void main(String[] args) {
		// 创建对象
		Student student = new Student();
		
		// 给对象赋值
		student.name = "xxx";
        // age是负数
		student.age = -21;
		
		// 打印信息
        // age是负数之类时也会正常打印，出现安全隐患
		System.out.println(student.name);
		System.out.println(student.age);		
	}
}
```

#### 8.2.2 private关键字概述

private是一个权限修饰符，代表最小权限

特点：

1. 可以修饰成员变量和成员方法

2. 被private修饰的成员变量或方法，只能在==本类中使用==，如果需要被其他类使用使用下列的操作

>“get变量名()”方法，用于获取成员变量的值，方法用public修饰
>
>”set变量名(参数)”方法，用于设置成员变量的值，方法用public修饰



```java
使用格式：
    修饰成员变量
    private 数据类型 变量名;
	
	修饰成员方法：
    private 返回值类型 方法名(参数列表){
        代码;
    }
```

#### 8.2.3 set和get方法

```java
// 学生类
public class Student {
	// 成员变量
	private String name;
	private int age;
	String grade;
	
	public void setName(String s) {
		name = s;
	}	
    
	public String getName() {
		return name;
	}
    
	public void setAge(int s) {
		if (s < 0 || s > 150) {
			System.out.println("输入的数据不合法");
		}else {
			age = s;
		}
	}
	
	public int getAge() {
		return age;
	}
    
    // 方法
	public void study(String name){
		System.out.println(name + "正在学习中，请勿打扰...");
	}
	
	public void lessons(String name, String lesson) {
		System.out.println(name + "正在教学楼上" + lesson + "课");
	}
}

// 学生测试类
public class StudentTestDrive {
	public static void main(String[] args) {
		// 创建对象
		Student student = new Student();
		
		
		// 给对象赋值
		student.setName("xxx");
		student.setAge(21);
		
		// 取值
		String name = student.getName();
		int age = student.getAge();
		student.grade = "四年级";
		
		
		// 输出信息
		System.out.println(name);
		System.out.println(age);
		System.out.println(student.grade);
		
		// 方法
		student.study("xxx");
		student.lessons("xxx", "英语");
	}
}
```

### 8.3 为什么要对属性进行封装

通过对象名直接访问成员变量的方式对属性赋值，会存在安全隐患！

解决方法：不让外界直接访问成员变量（也就是要对属性进行封装/隐藏）

#### 8.3.1 对成员变量封装的步骤：

1. 使用private关键字修饰成员变量
2. 使用公共的访问方法
   - 给成员变量赋值的公共方法（set方法）
   - 给成员变量值的公共方法（get方法）

### 8.4 this关键字

用途：解决实例变量（private String name）和局部变量(setName(String name))之间发生的同名的冲突

this的含义与使用：

this的含义：this代表当前调用方法的引用**，哪个对象调用this所在的方法，this就代表哪个对象**

this的主要作用：**区别同名的成员变量和局部变量**

```java
// 不加this时，自己赋值给自己，不使用成员变量
public class Student {
	// 成员变量
	private String name;
	private int age;
	String grade;
	
	public void setName(String name) {
		name = name;
	}	
    
	public String getName() {
		return name;
	}
    
	public void setAge(int age) {
		if (age < 0 || age > 150) {
			System.out.println("输入的数据不合法");
		}else {
			age = age;
		}
	}
	
	public int getAge() {
		return age;
	}
}

// 加this
public class Student {
	// 成员变量
	private String name;
	private int age;
	String grade;
	
	public void setName(String name) {
		this.name = name;
	}	
    
	public String getName() {
		return name;
	}
    
	public void setAge(int age) {
		if (age < 0 || age > 150) {
			System.out.println("输入的数据不合法");
		}else {
			this.age = age;
		}
	}
	
	public int getAge() {
		return age;
	}
}
```

### 8.5 构造方法的定义和调用

#### 8.5.1 概念

构造方法是一种特殊的方法，主要是完成对象的创建，对象数据的初始化。在创建对象（new运算符）之后自动调用

#### 8.5.2 格式

```java
// 空参构造方法
修饰符 类名(){
    
}

// 有参构造方法
修饰符 类名(修饰符){
    方法体;
}
```

#### 8.5.3 特点

1. 方法名必须和它所在的类名相同
2. 可以有多个参数
3. **没有任何返回值，包括void**
4. 默认返回值类型就是对象类型本身
5. **只能与new运算符结合使用**

```java
// 例子：
//空参构造方法
public Studnet() {
	System.out.println("调用了空参构造");
}
	
//有参构造方法
public Studnet(String name,int age){
	this.name = name;
	this.age = age;
}
```

```java
// 使用
Studnet stu2 = new Studnet();
		
Studnet stu3 = new Studnet("李四",19);
```

#### 8.5.4 构造方法的注意事项

1. 如果没有定义构造方法，系统将给出一个默认的无参构造方法，且方法体为空
2. 如果定义了构造方法，系统将不再提供默认的构造方法
3. 构造方法可以重载，既可以定义参数，也可以不定义参数
4. **构造方法只能给属性赋值一次**，set方法可以给属性赋值无数次

>构造方法不能被 ==static、final、synchronized、abstract 和 native（类似于 abstract）修饰==。构造方法用于初始化一个新对象，所以用 static 修饰没有意义。构造方法不能被子类继承，所以用 final 和 abstract 修饰没有意义。多个线程不会同时创建内存地址相同的同一个对象，所以用 synchronized 修饰没有必要

## 9、标准类制作

JavaBean是java语言提供的一种标准规范。符号JavaBean的类，要求类必须是公共的，属性使用private修饰，并且具有无参构造方法，提供用来操作成员变量的get，set方法

```java
public class 类名{
    // 成员变量，private
    // 构造方法
    // 无参构造方法：必须
    // 有参构造方法：根据需求给
    
    // getXxx()
    // setXxx()
    
    // 成员方法
}
```

## 10、API的使用

#### 10.1 API介绍

应用程序编程接口，**Java API是一本程序员的字典**，是JDK中提供给我们的使用类的**说明文档**

#### 10.2 API使用步骤

1. 打开API文档
2. 点击显示
3. 点击索引，在输入框中输入要查的类或者接口
4. 查看类的包，如果在java.lang包不需要导入，其他包都需要的导入
5. 查看类的解释说明
6. 查看类的构造方法
7. 查看类的成员方法