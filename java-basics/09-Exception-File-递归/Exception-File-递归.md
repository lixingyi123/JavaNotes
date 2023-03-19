<p align = "center" ><font size = 10， color = "#009999">Exception & File & 递归</font></p>

## 1、异常

### 1.1 异常的概念

异常：指的是在程序的执行过程中，出现了非正常的情况，最终会导致jvm的非正常停止

**注意：**在java等面向对象的编程语言中，异常本身是一个类，产生异常就是创建异常对象并抛出了一个异常对象。**Java处理异常的方式是中断处理**（直接终止程序的运行，把异常信息打印到控制台上）

==注意：==

异常指的并不是语法错误。语法错了，编译不通过，不会产生字节码文件，根本不能运行

### 1.2 异常的体系

java.lang类的Throwable：异常的根类，其下有两个子类

Throwable体系：

Errow：严重的错误，无法处理的错误，只能事先避免。例如：服务器崩溃，数据库崩溃

Exception：表示异常，异常产生后程序员可以通过修改代码对异常进行处理，是必须要处理的

![](https://github.com/lixingyi123/JavaNotes/blob/main/java-basics/09-Exception-File-%E9%80%92%E5%BD%92/images/%E5%BC%82%E5%B8%B8%E4%BD%93%E7%B3%BB.png?raw=true)

### 1.3 异常的分类

Exception分类：根据在编译时期还是运行时期去检查异常

**编译时异常**：checked异常，在编译时期就会检查，如果没有处理异常，则编译失败（格式之类的异常）

**运行时异常**：runtime异常，在运行期间，检查异常，在编译时不会出现异常

### 1.4 异常产生过程

![](https://github.com/lixingyi123/JavaNotes/blob/main/java-basics/09-Exception-File-%E9%80%92%E5%BD%92/images/%E5%BC%82%E5%B8%B8%E4%BA%A7%E7%94%9F%E8%BF%87%E7%A8%8B.png?raw=true)

## 2、异常的产生与处理

在Java中，提供了一个throw关键字，用来抛出一个指定的异常对象

throw用在方法内，用来抛出一个异常对象，将这个异常对象传到调用者处，结束当前方法的执行。

### 2.1 throw关键字的使用格式

throw关键字的**使用格式**：

```java
throw new 异常类名(参数)

例如：
    throw new ArrayIndexOutOfBoundsException("出现异常:" + index);
```

```java
public class ExceptionDemo {
	public static void main(String[] args) {
		int[] arr = {1, 3, 56, 67};
		int num = getElement(arr, 4);
		System.out.println(num);
	}
	
	public static int getElement(int[] arr, int index) {
		if (index < 0 || index > arr.length - 1) {
			throw new ArrayIndexOutOfBoundsException("出现异常:" + index);
		}else {
			int element = arr[index];
			return element;
		}
	}
}

结果：
    Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: 出现异常:4
```

### 2.2 声明处理异常

#### 2.2.1 声明处理异常的格式

```java
修饰符 返回值类型 方法名(参数) throws 异常类名1, 异常类名2{
    
}
```

使用**throws**关键字将问题标识出来，表示当前方法不处理异常，而是提醒给调用者，让调用者处理....最终会到虚拟机，虚拟机直接结束程序，打印异常信息。

```java
public class Test{
    public static void main(String[] args) throws ParseException{
        show();
    }
    
    public static void show() throws ParseException{
        // 一般用来处理编译时异常，让程序通过编译，但程序运行的时候出现异常，程序还是无法继续向下执行
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");
        sdf.parse("1999年4月6日");
        System.out.println("aaaa");
    }
}
```

### 2.3 try - catch捕获处理异常

捕获处理异常，对异常进行捕获处理，处理完成后程序可以正常向下执行

格式：

```java
try{
    // 可能出现异常的代码
}catch(异常类型 e){
    处理异常的代码
    // 打印异常信息
}

执行步骤：
    1.首先执行try中的代码，如果try中的代码出现了异常，那么就直接执行catch()中的代码，执行完后，程序继续向下执行
    2.如果try中没有出现异常，那么就不会执行catch()中的代码，接着向下执行
```

```java
import java.text.ParseException;

public class Test1 {
	public static void main(String[] args) {
		method1();
		
		try {
			System.out.println(1/1);// 没有出现异常，正常执行代码
		}catch (Exception e) {
			System.out.println("出现了算数异常");
		}
		
		try {
			System.out.println(1/0);// 出现异常，直接执行catch里的代码，执行完毕后就退出try-catch
            System.out.println(1/1);// 不会执行
		}catch(Exception e) {
			System.out.println("出现算数异常");
		}
		System.out.println("main方法结束");// 正常执行
	}
		
		
	}
	
	public static void method1() {
		try {
			throw new ParseException("解析异常", 1);
		}catch (ParseException e) {
			System.out.println("出现了异常");
		}
		System.out.println("方法结束");
		
	}

}

结果：
出现了异常
方法结束
1
出现算数异常
main方法结束
```

#### 2.3.1 try-catch注意事项

1. try和catch不能单独使用，必须组合使用
2. try中的代码出现了异常，那么出现异常位置后的代码不会执行
3. 捕获处理异常，如果程序出现了异常，程序会继续向下执行
4. 声明处理异常，如果程序出现了异常，程序不会向下继续执行

#### 2.3.2 获取异常信息

不需要我们写，一般会自动在控制台输出

```java
// 方法
String getMassage();
    获取异常的描述信息，原因（提示给用户），就是提示错误原因

String toString();
	获取异常的类型和异常描述信息（不用）

void printStackTrace();
  将此throwable及其追踪至具体错误位置
  包含了异常的类型，原因。还包括异常出现的位置，在开发和调试阶段，都要使用printStackTrace。
```

```java
public class Test1 {
	public static void main(String[] args) {
		try {
			System.out.println(1/0);
		}catch(Exception e) {
			System.out.println(e.getMessage());// 获取异常信息
			
            System.out.println();
			System.out.println(e.toString());
            
			System.out.println();
			e.printStackTrace();
		}
		System.out.println("main方法结束");
	}
}


结果：
/ by zero

java.lang.ArithmeticException: / by zero

java.lang.ArithmeticException: / by zero
	at net.wanhe.day11.Test1.main(Test1.java:8)

main方法结束
```

### 2.4 finally代码块

有一些特定的代码，无论是否发生异常，都需要执行，因为异常会引发程序跳转，导致有些语句执行不到，finally可以解决这个问题，在finally中的代码是一定会被执行的

格式：

```java
try{
    // 可能引发异常的代码
}catch(异常类型 e){
    处理异常的代码；
}finally{
    // 一定会执行的代码块
    // 一般用来释放资源
}

执行步骤:
	1.首先执行try中的代码，如果try中的代码出现了异常，那么就直接执行catch()中的代码，执行完catch()后，执行finally中的代码
    2.如果try中没有出现异常，那么就不会执行catch()中的代码，但是会执行finally中的代码
```

**注意：finally不能单独执行**

```java
public class Test1 {
	public static void main(String[] args) {
		try {
			System.out.println(1/0);
		}catch(Exception e) {
			System.out.println("出现异常");
		}finally{
			System.out.println("执行finally代码。。。");
		}
		System.out.println();
		System.out.println("main方法结束");
	}
}

结果：
出现异常
执行finally代码。。。

main方法结束
```

#### 2.4.1 异常注意事项

多个异常使用捕获方式：

**一般使用多个异常一次捕获，多次处理** 

```java
try{
    // 可能出现异常的代码块
}catch(异常类型1 e){
    处理异常的代码
	System.out.println("catch出现了异常");
}catch(异常类型2 e){
    处理异常的代码
	System.out.println("catch出现了异常");
}finally{
    
}
```

```java
import java.io.FileNotFoundException;
import java.text.ParseException;

public class Test02 {
	public static void main(String[] args) {
		
	}
	
	public static void show1() {
		//1.运行时异常可以不处理，可以既不捕获也不声明
		System.out.println(1/0);
		
	}

	//声明处理多个异常，可以直接声明这多个异常的父类
	public static void show2(int num) throws Exception {
		
		if(num == 1) {
			throw new FileNotFoundException("");
		}else {
			throw new ParseException("", 1);
		}
	}
	
	//当多个异常分别处理，捕获处理，前面的类不能是后面类的父类
	public static void show3(int num) {
		try {
			if(num == 1) {
				throw new FileNotFoundException("");
			}else {
				throw new ParseException("", 1);
			}
		} catch (FileNotFoundException e) {
			// TODO: handle exception
		} catch (ParseException e) {
			// TODO: handle exception
		}
		
		try {
			if(num == 1) {
				throw new FileNotFoundException("");
			}else {
				throw new ParseException("", 1);
			}	
		} catch(FileNotFoundException e){
			System.out.println("出现异常了");
		}catch(ParseException e){
			System.out.println("出现异常了");
		}catch(Exception e){
			System.out.println("出现异常了");
		}
	}
}
```

注意：

1. 运行时异常可以不处理，可以既不捕获又不声明
2. 如果父类中方法抛出了异常，子类重写父类方法，只能抛出相同的异常或者它的子集
3. 如果父类方法没有抛出异常。子类重写父类方法，只能捕获处理，不能声明抛出
4. 声明处理多个异常，可以直接声明这多个异常的父类  
5. 当多个异常分别处理，捕获处理，前面的类不能是后面的父类

### 2.5 自定义异常

#### 2.5.1 分类（常用）

1. 自定义一个编译时异常，自定义一个类，继承Exception
2. 自定义一个运行时异常的类，然后继承RuntimeException

``` java
public static void main(String[] args){
    int age = -18;
    if(age < 0 || age > 140){
        throw new MyException("自定义异常")
    }
}
```

## 3、File类

java.io类File类是文件和目录路径名的抽象表示，主要用于文件的创建，删查改的操作

### 3.1 构造方法

```java
File(File parent, String child) 
从父抽象路径名和子路径名字符串创建新的 File实例。
    
File(String pathname) 
通过将给定的路径名字符串转换为抽象路径名来创建新的 File实例。
    
File(String parent, String child) 
从父路径名字符串和子路径名字符串创建新的 File实例。
```

```java
import java.io.File;

public class Test3 {
	public static void main(String[] args) {
		// 创建file文件
		// File(String pathname)
		File file = new File("D:\\images\\top.jpg");
		
		// File(String parent, String child)
		File file2 = new File("D:\\images", "top.jpg");
		
		
		// File(File parent,String child)
		File parent = new File("D:\\images");
		File file3 = new File(parent, "top.jpg");
		
		System.out.println(file);
		System.out.println(file2);
		System.out.println(file3);
		
		System.out.println("-------------");
		
		// 路径不存在
		File file4 = new File("D:\\image\\344");
		System.out.println(file4);
	}

}
```

#### 3.1.1 构造方法注意事项

1. 一个file对象代表硬盘中的一个文件或者一个目录
2. 无论该路径是否存在文件或者目录，都会创建

### 3.2 绝对路径与相对路径

相对位置：是最常用的，相对于该项目目录的路径，是一个便捷的路径

绝对路径：从盘符开始，是一个完整的路径

```java
绝对路径：D:\java\\images\aaa.txt
相对路径：images\aaa.txt
```

### 3.3 功能方法

#### 3.3.1 判断功能方法

```java
// 检查文件是否存在
boolean exists() 
   测试此抽象路径名表示的文件或目录是否存在。

// 检查是否是目录
boolean isDirectory() 
测试此抽象路径名表示的文件是否为目录。  
  
// 检查是否是普通文件
boolean isFile() 
测试此抽象路径名表示的文件是否为普通文件。  
```

#### 3.3.2 创删文件/文件夹方法

```java
// 创建文件
boolean createNewFile() 
  当且仅当具有该名称的文件尚不存在时，原子地创建一个由该抽象路径名命名的新的空文件。 
    
// 创建文件夹
boolean mkdir() 
  创建由此抽象路径名命名的目录。  
boolean mkdirs() 
  创建由此抽象路径名命名的目录，包括任何必需但不存在的父目录。  
// 删除文件或空文件夹
boolean delete() 
  删除由此抽象路径名表示的文件或目录。  
```

```java
import java.io.File;
import java.io.IOException;

public class Test3 {
	public static void main(String[] args) throws IOException {
		// 创建file文件
		// File(String pathname)
		File file = new File("aaa\\top.txt");
		System.out.println(file.createNewFile());
		
		// 也是创建文件，默认是txt型文件
		File file1 = new File("aaa\\bbb");
		System.out.println(file1.createNewFile());
		
		// 创建文件夹单目录
		File file2 = new File("aaa\\eee");
		System.out.println(file2.mkdir());
		
		// 创建文件夹多目录
		File file3  = new File("aaa\\eee\\ccc");
		System.out.println(file3.mkdirs());// true
		
		//删除文件或空文件夹
		// 删除文件
		System.out.println(file1.delete());// true
		
		// 删除非空文件夹
		System.out.println(file2.delete());// false
		
		// 删除空文件夹
		System.out.println(file3.delete());// true
	}

}
```

#### 3.3.3 File类遍历目录方法

```java
// 返回一个字符串数组
String[] list()
    返回一个字符串数组，命名由此抽象路径名表示的目录中的文件和目录。
    
// 返回一个文件夹路径名数组
File[] listFiles() // 常用
	返回一个抽象路径名数组，表示由该抽象路径名表示的目录中的文件。  
```

```java
import java.io.File;
import java.io.IOException;

public class Test3 {
	public static void main(String[] args) throws IOException {
		// String[] list()
		File file = new File("aaa");
		String[] arrs = file.list();
		for (String arr : arrs) {
			System.out.println(arr);
		}
		
		// File[] listFiles() 
		System.out.println("-----------");
		File[] f = file.listFiles();
		for (File f1 : f) {
			System.out.println(f1);
		};		 
	}
}

结果：
eee
top.txt
-----------
aaa\eee
aaa\top.txt
```

#### 3.3.4 File获取功能的方法

```java
// 得到某个文件的绝对路径
String getAbsolutePath() 
	返回此抽象路径名的绝对路径名字符串。 
    
// 返回路径的文件名称
String getName() 
	返回由此抽象路径名表示的文件或目录的名称。 
 
// 将路径转化为String型
String getPath() 
    将此抽象路径名转换为一个路径名字符串。

// 返回字符串的长度
long length() 
    返回由此抽象路径名表示的文件的长度。
```

```java
import java.io.File;

public class Test4 {
	public static void main(String[] args) {
		File file = new File("aaa\\top.txt");
		// 将file路径转化为String型
		String str = file.getPath();
		System.out.println(str);
		
		// 获取file的绝对路径
		System.out.println(file.getAbsolutePath()); // 绝对路径
		
		// 获取路径的名称
		System.out.println(file.getName()); // top.txt
		
		// 返回file文件的长度
		System.out.println(file.length()); // 文件里为空，结果为0
	}
 
}
```

## 4、递归

程序中的递归：指在当前方法中**自己调用自己**的这种现象

### 4.1 递归的注意事项

1. 递归要有出口（结果方法）,否则会栈溢出
2. 递归的出口不能太晚了

```java
public class Test4 {
	static int count = 0;
	public static void main(String[] args) {
		method();
		
	}
	
	public static void method() {
		count++;
		if(count == 5) {
			return;
		}
		System.out.println(count);
		method();
	}
 
}
```

### 4.2 练习

```java
//练习1： 计算n的和
public class Test4 {
	public static void main(String[] args) {
		int n = 3;
		System.out.println(getSum(n));
	}
	
	public static int getSum(int n) {
		if(n == 1) {
			return 1;
		}
		
		return n + getSum(n-1);
		
	}
}

// 练习2：求n的阶乘
public class Test{
    public static void main(String[] args){
        System.out.println(jiecheng(4));
    }
    
    public static int jiecheng(int n){
        if(n == 1){
            return 1;
        }
        return n * jiecheng(n - 1);
    }
}


// 练习3：递归输出src目录下所有以.java结尾的文件的绝对路径
import java.io.File;
import java.util.Arrays;

public class Test4 {
	public static void main(String[] args) {
		
		File file = new File("src");
		printFile(file);
	}
	
	public static void printFile(File file) {
		// 在方法中，获取该目录下的所有文件与目录
		File[] files = file.listFiles();
		
		// 循环遍历获取到的所有子文件与目录
		if (files != null) {
			// 判断遍历出来的是子文件还是目录
			for (File f : files) {
				// 如果是文件，判断文件是否以.java结尾
				if(f.isFile() && f.getName().endsWith(".java")) {
                    // System.out.println(f); 得到的是相对路径
                    // f.getAbsolutePath()得到文件的绝对路径
					System.out.println(f.getAbsolutePath());
				}
				
				if (f.isDirectory()) {
					printFile(f);
				}
			}
		}
		
	}
 
}
```