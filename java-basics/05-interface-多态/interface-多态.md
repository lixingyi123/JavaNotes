<p align = "center" ><font size = 10， color = "#009999">Interface & 多态</font></p>

## 1、接口

### 1.1 接口的介绍

#### 1.1.1 接口定义与特点

**接口：**如果一个类中都是抽象方法，那么这个类应该是定义规则的类，那么这个类应该是定义规则的类，我们就把此类定义为接口，接口是一种引用数据类型

**作用**：

1. 用于定义规则
2. 程序的扩展性

**接口的定义和特点：**

1. 定义接口的关键字使用==interface==

   public **interface** 接口名 [extends 其他的接口名]{

   }

2. 类与接口之间的关系是实现关系，用==关键字implements==进行连接

​		public class  类名 implements 接口名{

​		}

3. 特点：
   - 接口不能实例化
   - 接口的子类我们叫做实现类
     - 要么重写接口中的所有抽象方法
     - 要么实现类是一个接口

4. **注意：**类与接口之间关系就是实现关系，**一个类可以实现多个接口，使用逗号隔开**，还有可以在继承一个类的同时，实现多个接口。

```java
public interface InterA{
    // 在接口中写两个抽象类
    public abstract void show();
    public abstract void method();
}

public interface InterB{
    
}

public class InterImpl implements InterA, InterB{
	@Override
    public void show(){
        
    }
    
    @Override
    public void method(){
        
    }
}
```

#### 1.1.2 接口的成员特点

1. **成员变量**：都是常量，写与不写都有默认修饰符**public static final**

2. 构造方法：没有构造方不过合计法

3. 成员方法：只能是抽象方法，写与不写都有默认修饰符**public abstract**

4. 接口中的方法是不能在接口中实现的，只能由实现接口的类去实现接口中的方法

jdk1.8之前：只能是抽象方法

jdk1.8之后：默认方法：解决接口升级的问题，静态方法

jdk1.9版本：私有方法：抽取默认方法中的共性内容

##### 1.1.2.1 抽象类和接口的使用

```java
举例：
    狗
    行为：吼叫，吃饭，睡觉
    
	缉毒犬：特有行为：缉毒
    行为：吼叫，吃饭，睡觉
    
    泰迪：
    行为：吼叫，吃饭，睡觉
```

```java
// Dog抽象类
public abstract class Dog {
    // 抽象方法，用于所有继承的类都必须重写此方法
	public abstract void roar();
    
	public void sleep() {
		System.out.println("睡觉");
	}
}

// JiDu类，接口类
public interface JiDu {
	void jiDu();// 写不写都默认是abstract类

}

// JiDuDog类，继承Dog类，实现JiDu类，先写继承再写实现
public class JiDuDog extends Dog implements JiDu{

	@Override
	public void jiDu() {
		// TODO Auto-generated method stub
		System.out.println("缉毒犬在缉毒工作中");
	}

	@Override
	public void roar() {
		// TODO Auto-generated method stub
		System.out.println("缉毒犬在叫....");
	}
}

// TaiDi类，继承Dog类
public class TaiDi extends Dog {

	@Override
	public void roar() {
		// TODO Auto-generated method stub
		System.out.println("泰迪在叫");
	}
}

// 测试类
public class Text {
	public static void main(String[] args) {
		JiDuDog jidu = new JiDuDog();
		jidu.roar();
		jidu.jiDu();
		
		TaiDi taidi = new TaiDi();
		taidi.roar();
        taidi.sleep();
	}
}
```

**小结：**

**额外的功能（特有的功能）**-->定义在**接口**中，让实现类去实现

**共性的功能**-->在父类中定义，让子类去继承

## 2、多态  

**多态是继封装，继承之后，面向对象的第三大特征**

**同一种行为**，通过不同的事物，可以体现出不同的形态，多态，就是描述这样的状态

**定义：**

​		**多态：**是指同一行为，对于不同的对象具有多个不同表现形式

​		**程序中的多态：**是指同一个方法，对于不同的对象具有不同的实现

前提条件：

​		1. 要满足继承或者实现

​		2. 父类引用指向子类对象\接口引用指向实现类对象（格式体现）

​		3. 方法的重写（不重写，无意义）

### 2.1 多态的实现

#### 2.1.1 多态的体现：父类的引用指向它的子类对象

```java
父类类型 变量名 = new 子类对象;
变量名.方法名();
```



```java
class Animal{
	public void eat() {
		System.out.println("吃东西");
	}
}

class Dog extends Animal {

	@Override
	public void eat() {
		// TODO Auto-generated method stub
		System.out.println("狗吃骨头");
	}
}

class Cat extends Animal{

	@Override
	public void eat() {
		// TODO Auto-generated method stub
		System.out.println("猫吃鱼");
	}
	
}
public class Test {
	public static void main(String[] args) {
		// 父类引用指向子类对象
		Animal ani = new Dog(); // 多态
		ani.eat(); // 狗吃骨头
		
		Animal anl = new Cat();
		anl.eat(); // 猫吃鱼
	}
}
```

#### 2.1.2 多态时访问成员的特点

```java
class Animal{
	int num = 10;
	public void method1() {
		System.out.println("Animal 非静态方法");
	}
	
    // 静态方法
	public static void method2() {
		System.out.println("Animal 静态方法");
	}
}

class Dog extends Animal {
	int num = 20;
    
	@Override
	public void method1() {
		// TODO Auto-generated method stub
		System.out.println("Dog 非静态方法");
	}
	public static void method2() {
		// TODO Auto-generated method stub
		System.out.println("Dog 静态方法");
	}
}

public class Test {
	public static void main(String[] args) {
		// 父类引用指向子类对象
		Animal ani = new Dog();
		// 成员变量：编译看父类，运行看父类
		System.out.println(ani.num);// 10
		
		// 非静态方法：编译看父类，运行看子类
		ani.method1(); // Dog 非静态方法
		
		// 静态方法：编译看父类，运行看父类
		ani.method2();// Animal 静态方法
		
		// 结论：除了非静态方法是编译看父类，运行看子类，其他都是编译看父类，运行看父类
	}
}
```

小结：

```java
1.成员变量：编译看父类，运行看父类
2.非静态方法：编译看父类，运行看子类		
3.静态方法：编译看父类，运行看父类
    
结论：除了非静态方法是编译看父类，运行看子类，其他都是编译看父类，运行看父类
```

### 2.2 多态的表现形式

#### 2.1.1 普通父类多态

```java
class A{
}

class B extends A{
    
}

public class Test{
    public static void main(String[] args){
        A a = new B(); // 左边是一个父类
    }
}
```

#### 2.1.2 抽象父类多态

```java
abstract class A{
    
}

class B extends A{
    
}

public class Test{
    public static void main(String[] args){
        A a = new B(); // 左边是一个父类
    }
}
```

#### 2.1.3 父接口多态

```java
interface A{
    
}

class B implements A{
    
}

public class Test{
    public static void main(String[] args){
        A a = new B();
    }
}
```

### 2.3 多态的应用场景

#### 2.3.1 变量多态

**变量多态：**父类类型的变量指向子类类型的对象
	如果变量类型为父类类型，该变量可以接收该父类类型的对象，或者其所有的子类对象

```java
class Animal{
	public void eat() {
		System.out.println("吃东西");
	}
}

class Dog extends Animal {

	@Override
	public void eat() {
		// TODO Auto-generated method stub
		System.out.println("狗吃骨头");
	}
}

class Cat extends Animal{

	@Override
	public void eat() {
		// TODO Auto-generated method stub
		System.out.println("猫吃鱼");
	}
	
}
public class Test {
	public static void main(String[] args) {
		// 父类类型的变量指向子类类型的对象
		Animal ani = new Dog(); // 多态
		ani.eat(); // 狗吃骨头
		
		Animal anl = new Cat();
		anl.eat(); // 猫吃鱼
	}
}
```

#### 2.3.2 形参多态

**形参多态：**参数类型为父类类型，该参数就可以接收该父类类型的对象，或者是其所有子类对象

```java
class Animal{
	public void eat() {
		System.out.println("吃东西");
	}
}

class Dog extends Animal {

	@Override
	public void eat() {
		// TODO Auto-generated method stub
		System.out.println("狗吃骨头");
	}
}

class Cat extends Animal{

	@Override
	public void eat() {
		// TODO Auto-generated method stub
		System.out.println("猫吃鱼");
	}
	
}
public class Test {
	public static void main(String[] args) {
		// 父类类型的变量指向子类类型的对象
		Dog dog = new Dog(); 
		dog.method(); 
		
		Cat cat = new Cat();
		cat.method(); 
        
	}
    
    public static void method(Animal anl){
        
    }
}
```

#### 2.3.3 返回值多态

```java
class Animal{
	public void eat() {
		System.out.println("吃东西");
	}
}

class Dog extends Animal {

	@Override
	public void eat() {
		// TODO Auto-generated method stub
		System.out.println("狗吃骨头");
	}
}

class Cat extends Animal{

	@Override
	public void eat() {
		// TODO Auto-generated method stub
		System.out.println("猫吃鱼");
	}
	
}
public class Test {
	public static void main(String[] args) {
		// 父类类型的变量指向子类类型的对象
		Animal anl = method();
		anl.eat();
	}
    
    public static Animal method(){
        return new Cat();
    }
}
```

### 2.4 多态的好处与弊端

好处：提高了代码的扩展性

弊端：多态的情况下，只能调用父类的共性内容，不能调用子类特有的内容

### 2.5 引用类型转换

#### 2.5.1 向上转型

子类类型向父类类型向上转换的过程，这个过程是默认的

==Animal anl = new Cat();==

#### 2.5.2 向下转型

父类类型向子类类型向下转换的过程，这个过程是强制的

> ==Animal anl = new Cat()；==
>
> ==Cat c = (Cat) anl;==

#### 2.5.3 注意

```java
class Animal{
	public void eat() {
		System.out.println("吃东西");
	}
}

class Dog extends Animal{
	@Override
	public void eat() {
		System.out.println("狗吃骨头");
	}
	
	public void lookHome() {
		System.out.println("狗看家");
	}
}

class Cat extends Animal{
	@Override
	public void eat() {
		System.out.println("猫吃鱼");
	}
}

class person{
	
}
public class Test {
	public static void main(String[] args) {
		//父类引用指向子类对象
		//向上转型
		Animal anl = new Dog();//多态
		
		//向下转型
		Dog dog = (Dog)anl;
		dog.lookHome();
		
		System.out.println("***************************");
		Animal anl2 = new Cat();
		Dog d2 = (Dog)anl2;//运行报错，类型准换异常
		
		System.out.println("*************************");
		//Animal anl3 = new person();//编译报错，因为Animal和person不是父子关系
		
	}
}
```

#### 2.5.4 instanceof关键字

向下转型有风险，在转换前做一些验证

**格式：**

```java
变量名 instanceof 数据类型

// 判断anl是否能转换为Cat类型，如果可以返回true，否则返回false
if(anl instanceof Cat){
    Cat c = (Cat)anl;
}
```

```java
class Animal{
	public void eat() {
		System.out.println("吃东西");
	}
}

class Dog extends Animal{
	@Override
	public void eat() {
		System.out.println("狗吃骨头");
	}
	
	public void lookHome() {
		System.out.println("狗看家");
	}
}

class Cat extends Animal{
	@Override
	public void eat() {
		System.out.println("猫吃鱼");
	}
}

class person{
	
}

public class Test {
	public static void main(String[] args) {
	
		Animal anl = new Dog();

		if(anl instanceof Cat) {
			Cat c = (Cat)anl;
			
			System.out.println("转换。。。");
		}
		
		System.out.println("结束");
	}
}
```

## 3、内部类

将一个类A定义在另一个类B，里面的A就成为了内部类，B称为外部类

```java
class B{
    // 内部类
    class A{
        
    }
}
```

**特点：**

内部类可以直接访问外部类的成员，包括私有成员

外部类要访问内部内的成员，必须建立内部类的对象

```java
public class Body{
    // 成员变量
    private int numBody = 100;
    
    // 外部类方法
    public void methodBody1(){
        System.out.println("外部类的成员方法，methodBody1");
    }
    
    // 访问内部类的变量和方法
    public void methodBody2(){
        // 必须创建对象
        Head head = new Head();
        System.out.println(head.num);
        head.methodHead1();
    }
    
    // 内部类
    public class Head{
        // 内部类成员变量
        int num = 20;
        public void methodHead1(){
            System.out.println("内部类的成员方法，methodHead1");
        }
        // 访问外部类的变量和方法
        public void methodHead2(){
            System.out.println(numBody);
            methodBody1();
        }
    }
}


// main方法
public class Test{
	public static void main(String[] args){
        // 创建内部类对象
        Body.Head bh = new Body().new Head();
        System.out.println(bh.num);
        
        Body body = new Body();
    }
}
```

### 3.1 匿名内部类

匿名内部类：是内部类的简化写法，本质是：带具体实现的**父类或者父接口**的匿名的**子类对象**

```java
abstract class Animal{
	public abstract void eat();
}


public class Test {
	public static void main(String[] args) {
		//创建Animal子类对象《===》animal类的匿名内部类
		//父类引用指向子类对象
		Animal anl = new Animal() {
			@Override
			public void eat() {
				System.out.println("狗吃骨头");
				
			}
		}; //Animal类的子类对象
		
		anl.eat();
	}
}
```

```java
interface A{
	public abstract void eat();
}


public class Demo {
	public static void main(String[] args) {
			new A() {
			@Override
			public void eat() {
				System.out.println("实现了接口中的eat方法");
			}
		}.eat();//匿名内部类的匿名对象调用eat方法
		
	}
}
```

### 3.2 小结

**基本类型可以作为成员变量、方法的参数、方法的返回值，当然引用类型也可以作为成员变量、方法的参数、方法的返回值**

## 4、权限修饰符

Java中提供了四种访问权限，使用不同的访问权限修饰符，被修饰的内容会有不同的访问权限。

public：公共的

protected：受保护的

（空的）：默认的

private：私有的

|           | 同一个类中 | 同一个包中 | 不同包子类 | 不同包中 |
| --------- | ---------- | ---------- | ---------- | -------- |
| public    | ✔️          | ✔️          | ✔️          | ✔️        |
| protected | ✔️          | ✔️          | ✔️          |          |
| 空        | ✔️          | ✔️          |            |          |
| private   | ✔️          |            |            |          |

小结：

public具有最大权限，private则是最小权限

​	成员变量：private

​	构造方法：public

​	成员方法：public

## 5、代码块

### 5.1 构造代码块

>格式：{}
>
>位置：类中，方法外
>
>执行：每次在调用构造方法的时候，就会执行
>
>使用场景：统计创建了多少个该类对象

```java
public class Person {
	
	{
		System.out.println("构造代码块执行了");
	}

}


package net.wanho.day08;

public class Test {
	public static void main(String[] args) {
		Person p1 = new Person();
		Person p2 = new Person();
		
	}
}
```

### 5.2 静态代码块

>格式：static{}
>
>位置：类中，方法外
>
>执行：当类被加载的时候执行，并且只执行一次
>
>使用场景：例如加载驱动，这种只需要执行一次的代码就可以放在静态代码块中

```java
public class Person {
	
	static {
		System.out.println("Person  静态代码块");
	}
		
}


public class Test {
	public static void main(String[] args) {
		Person p1 = new Person();
		Person p2 = new Person();
		
	}
}
```

### 5.3 局部代码块

>格式：{}
>
>位置：方法中
>
>执行：调用方法，执行到局部代码块的时候执行
>
>使用场景：节省内存空间，没有太大意义

```java
public class Test {
	public static void main(String[] args) {
		System.out.println("开始");
		
		{
			int num = 10;
			System.out.println("局部代码块");
		}//把局部代码块中的变量占用的空间释放掉
		
		System.out.println("结束");
	}
}
```

## 6、常用类

### 6.1 Object类

**概述**：java.lang.Object类是Java语言中的根类，是所有类的父类。

如果一个类没有特别指定父类，那么默认继承Object类

#### 6.1.1 toString方法

String toString():返回该对象的字符串表示，字符串内容：对象的类型名 + @ + 内存地址值

```java
public class Test {
	public static void main(String[] args) {
		Person p = new Person("张三",20);
		System.out.println(p);//net.wanho.day08.Person@15db9742
		System.out.println(p.toString());//net.wanho.day08.Person@15db9742
	}
}
```

由于toString方法返回的结果是内存地址，而在开发中，经常需要按照对象的属性得到相应的值，因此我们需要重写toString。

```java
public class Person {
	String name;
	int age;
	
	public Person() {
		super();
	}
    
	public Person(String name, int age) {
		super();
		this.name = name;
		this.age = age;
	}
	
	@Override
	public String toString() {
		return "name="+name+","+"age="+age;
	}	
}

package net.wanho.day08;

public class Test {
	public static void main(String[] args) {
		Person p = new Person("张三",20);
		System.out.println(p);//name=张三,age=20
	}
}
```

#### 6.1.2 equals方法

boolean equals（Object obj）：指示其他某个对象是否与此对象"相等"

**Object类的equals方法默认==比较，也就是比较的是两个对象的地址值，对于我们来说没有用。**

如果希望进行对象的内容比较，可以重写equals方法

##### 6.1.2.1 重写equals

```java
public class Person {
	String name;
	int age;
	
	
	public Person() {
		super();
	}


	public Person(String name, int age) {
		super();
		this.name = name;
		this.age = age;
	}

	@Override
	public String toString() {
		return "Person [name=" + name + ", age=" + age + "]";
	}

	@Override
	public int hashCode() {
		final int prime = 31;
		int result = 1;
		result = prime * result + age;
		result = prime * result + ((name == null) ? 0 : name.hashCode());
		return result;
	}

	@Override
	public boolean equals(Object obj) {
		if (this == obj)
			return true;
		if (obj == null)
			return false;
		if (getClass() != obj.getClass())
			return false;
		Person other = (Person) obj;
		if (age != other.age)
			return false;
		if (name == null) {
			if (other.name != null)
				return false;
		} else if (!name.equals(other.name))
			return false;
		return true;
	}	
	
}
现在的equals()方法是进行内容比较，而不是单纯的引用比较。
```
