<p align = "center" ><font size = 10， color = "#009999">I/O</font></p>

## 1、I/O流

I：代表input输入，从其他存储设备读数据到内存就是输入

O：代表output输出，从内存中写数据到其他存储设备

### 1.1 I/O分类

**根据数据的流向分类：输入流和输出流**

**输入流：**把数据从其他设备上读取到内存中的流

​		字节输入流：以字节为基本单位，读数据

​		字符输入流：以字符为基本单位，读数据

**输出流：**把数据从内存中写出到其他设备上的流

​		字节输出流：以字节为基本单位，写出数据

​		字符输出流：以字符为基本单位，写出数据



**根据数据的类型分类：字节流和字符流**

**字节流：**以字节为基本单位，读写数据

​		字节输入流：以字节为基本单位，读数据

​		字节输出流：以字节为基本单位，写出数据

**字符流：**以字符为基本单位。读写数据

​		字符输入流：以字符为基本单位，读数据

​		字符输出流：以字符为基本单位，写出数据

### 1.2 字节输出流OutputStream

Java.io类OutputStream抽象类表示**字节输出流的所有类的超类**，将制定的字节信息写到目的地，它定义了字节输出流的共性功能方法。

#### 1.2.1 OutputStream方法

```java
void close() 
	关闭此输出流并释放与此流相关联的任何系统资源。  

void write(byte[] b) 
	将 b.length字节从指定的字节数组写入此输出流。  
    
void write(byte[] b, int off, int len) 
	从指定的字节数组写入 len个字节，从偏移 off开始输出到此输出流。
    
abstract void write(int b) 
	将指定的字节写入此输出流。
```

### 1.3 FileOutputStream

#### 1.3.1 构造方法

**注意点**：

当我们创建一个流对象时，必须传入一个文件路径，该路径下，如果没有这个文件，就会创建该文件，如果有这个文件，会清空文件中的内容

```java
FileOutputStream(File file) 
	创建文件输出流以写入由指定的 File对象表示的文件。
    
FileOutputStream(String name) 
	创建文件输出流以指定的名称写入文件。 
```

```java
import java.io.File;
import java.io.FileOutputStream;

public class Test1 {
	public static void main(String[] args) throws Exception{
		// 创建字节输出流对象，会自动创建文件(String)
		// FileOutputStream(String name)
		FileOutputStream fos = new FileOutputStream("aaa\\eee\\a.txt");
		
		//FileOutputStream(File file)
		FileOutputStream fos1 = new FileOutputStream(new File("aaa\\eee\\b.txt"));
				
	}

}
```

#### 1.3.2 写出数据

##### 1.3.2.1 写出单个数据

```java
import java.io.File;
import java.io.FileOutputStream;

public class Test1 {
	public static void main(String[] args) throws Exception{
		// 创建字节输出流对象，会自动创建文件(String)
		// FileOutputStream(String name)
		FileOutputStream fos = new FileOutputStream("aaa\\eee\\a.txt");
		
		
		// 写出单个字节数据
		fos.write(97);
		fos.write(98);
		fos.write(99);
		
		
		// 释放资源
		fos.close();
	}

}
```

##### 1.3.2.2 写出字节数组

```java
import java.io.File;
import java.io.FileOutputStream;

public class Test1 {
	public static void main(String[] args) throws Exception{
		// 创建字节输出流对象，会自动创建文件(String)
		// FileOutputStream(String name)
		FileOutputStream fos = new FileOutputStream("aaa\\eee\\a.txt");
		
		byte[] arr = {97, 98, 99};
		
		// 写出字节数组
		fos.write(arr);
	
		// 释放资源
		fos.close();
	}
}
```

```java
import java.io.File;
import java.io.FileOutputStream;

public class Test1 {
	public static void main(String[] args) throws Exception{
		// 创建字节输出流对象，会自动创建文件(String)
		// FileOutputStream(String name)
		FileOutputStream fos = new FileOutputStream("aaa\\eee\\a.txt");
		
		
		// 写出字节数组
        // getBytes()将字符串转换为字符数组
		fos.write("你好，Hello".getBytes());
		fos.write("\r\n".getBytes()); // 换行
		fos.write("很好，good".getBytes());
		
		// 释放资源
		fos.close();
	}

}
```

##### 1.3.2.3 写出指定数组长度字节

```java
import java.io.File;
import java.io.FileOutputStream;

public class Test1 {
	public static void main(String[] args) throws Exception{
		// 创建字节输出流对象，会自动创建文件(String)
		// FileOutputStream(String name)
		FileOutputStream fos = new FileOutputStream("aaa\\eee\\a.txt");
		
        byte[] arr1 = {97, 98, 99, 144};
		
        // void write(byte[] b, int off, int len) 
        // 从指定的字节数组写入 len个字节，从偏移 off开始输出到此输出流。
        fos.write(arr1, 1, 2); // 2表示需要写入的个数，而不是索引
				
		// 释放资源
		fos.close();
	}
}
```

##### 1.3.2.4 数据追加续写

```java
FileOutputStream fos = new FileOutputStream("aaa\\eee\\a.txt", true);

解释：
   FileOutputStream(File file, boolean append)
     boolean append 默认为false。也就是运行时默认清空文件中的内容
     如果不想清空文件的内容，将append写为true
```

### 1.4 字节输入流InputStream

Java.io类InputStream抽象类是表示**输入字节流的所有类的超类**

#### 1.4.1 InputStream方法

```java
void close() 
关闭此输入流并释放与流相关联的任何系统资源。  
 
abstract int read() 
从输入流读取数据的下一个字节。 
    
int read(byte[] b) 
从输入流读取一些字节数，并将它们存储到缓冲区 b 。  
    
int read(byte[] b, int off, int len) 
从输入流读取最多 len字节的数据到一个字节数组。  
```

### 1.5 FileInputStream

#### 1.5.1 构造方法

```java
FileInputStream(File file) 
	通过打开与实际文件的连接创建一个 FileInputStream ，该文件由文件系统中的 File对象 file命名。  
 
FileInputStream(String name) 
	通过打开与实际文件的连接来创建一个 FileInputStream ，该文件由文件系统中的路径名 name命名。 
```

```java
import java.io.FileInputStream;

public class Test2 {
	public static void main(String[] args) throws Exception{
		// FileInputStream(String name)
		// 文件存在
		FileInputStream fis = new FileInputStream("aaa\\eee\\a.txt");
		
		// 文件不存在, 报错
        //  java.io.FileNotFoundException
		FileInputStream fis2 = new FileInputStream("aaa\\a.txt");
	}

}
```

#### 1.5.2 读取数据

##### 1.5.2.1 读取单个数据

read方法，从此输入流中读取一个数据字节，提升为int类型

```java
// 方法1：
import java.io.FileInputStream;

public class Test2 {
	public static void main(String[] args) throws Exception{
		// FileInputStream(String name)
		FileInputStream fis = new FileInputStream("aaa\\eee\\a.txt");
		
		// 读数据,返回一个字节
		int read = fis.read();
		System.out.println((char)read);
		read = fis.read();
		System.out.println((char)read);
		read = fis.read();
		System.out.println((char)read);
		// 读到末尾就返回-1
		read = fis.read();
		System.out.println(read);
	
	}

}

// 方法2：循环改进读取方式
// FileInputStream(String name)
FileInputStream fis = new FileInputStream("aaa\\eee\\a.txt");
		
// 读数据,返回一个字节
int read;		
while((read = fis.read()) != -1) {
	System.out.println((char)read);			
}
	fis.close();		
}
```

##### 1.5.2.2 读取指定数组长度数据

```java
每次读取b的长度的字节到数组中，返回读取到的有效字节个数，读取到末尾，返回-1
从此输入流中将最多 b.length 个字节的数据读入一个 byte 数组中。
```

```java
import java.io.FileInputStream;

public class Test2 {
	public static void main(String[] args) throws Exception{
		// FileInputStream(String name)
		FileInputStream fis = new FileInputStream("aaa\\eee\\a.txt");
		
		// 读数据,返回一个字节
		byte[] arr = new byte[2];
		
		int read = fis.read(arr);
		System.out.println(new String(arr, 0, read));// ab
		
		int read2 = fis.read(arr);
		System.out.println(new String(arr, 0, read2));//c
		
		
		int read3 = fis.read(arr);
		System.out.println(new String(arr));//报错，超出索引范围
		fis.close();	
	}
}
```

```java
public class Test2 {
	public static void main(String[] args) throws Exception{
		// FileInputStream(String name)
		FileInputStream fis = new FileInputStream("aaa\\eee\\a.txt");
		
		// 读数据,返回一个字节
		byte[] arr = new byte[2];
		
		int len; // 有效字节个数
        // 循环读取代码
		while((len = fis.read()) != -1) {
			System.out.println(new String(arr, 0, len));
		}
		fis.close();
	}

}
```

### 1.6 图片复制练习

```java
// 原理：先读取再写入
// 读取：其他设备传入内存
// 写入：内存写到其他设备
import java.io.FileInputStream;
import java.io.FileOutputStream;

public class Test3 {
	public static void main(String[] args) throws Exception{
		FileInputStream fis = new FileInputStream("aaa\\top.png");
		
		FileOutputStream fos = new FileOutputStream("aaa\\eee\\topCopy2.png");
		
		// 定义一个字节数组用来存储读取到的字节数据
		byte[] arr = new byte[8888];
		int len;
		// 循环读数据
		while((len = fis.read(arr)) != -1) {
			// 写出数据
			fos.write(arr, 0, len);
		}
		
		// 关闭资源,流的关闭原则，先开后关
		fos.close();
		fis.close();
	}

}
```

## 2、字符流

### 2.1 Reader

概述：java.io类Reader抽象类是用于表示读取字符流的所有类的超类，可以读取字符信息到内存中，它定义了字符输入流的基本共性功能方法。

#### 2.1.1 字符输入流常用方法

```java
// 释放资源
abstract void close() 
	关闭流并释放与之相关联的任何系统资源。  
 
// 读取字符
int read() 
   	读一个字符 
    
// 读取字符
int read(char[] cbuf) 
	将字符读入数组。  

abstract int read(char[] cbuf, int off, int len) 
	将字符读入数组的一部分。 
```

### 2.2 FileReader

![](https://github.com/lixingyi123/JavaNotes/blob/main/java-basics/10-IO/images/FileReader%E7%BB%A7%E6%89%BF%E4%BD%93%E7%B3%BB.png?raw=true)

#### 2.2.1 FileReader构造方法

```java
FileReader(File file) 
创建一个新的 FileReader ，给出 File读取。  

FileReader(String fileName) 
创建一个新的 FileReader ，给定要读取的文件的名称。  
```

**在读取数据时必须要存在文件，即文件路径正确才能读取，否则会报错FileNotFoundException**

```java
import java.io.FileReader;

public class Test3 {
	public static void main(String[] args) throws Exception{
		
		// 存在文件
		// 创建字符输入流对象，关联数据源文件路径
		FileReader fileReader = new FileReader("aaa\\top.txt");
		
		// 文件不存在
		FileReader fileReader1 = new FileReader("aaa\\eee\\top.txt");// FileNotFoundException
		
	}

}
```

#### 2.2.2 FileReader读取数据

##### 2.2.2.1 单个字符读取

读取字符：read方法，每次可以读取一个字符数据，int类型，当读到末尾时，返回-1

```java
import java.io.FileReader;

public class Test3 {
	public static void main(String[] args) throws Exception{
		
		// 存在文件
		// 创建字符输入流对象，关联数据源文件路径
		FileReader fileReader = new FileReader("aaa\\top.txt");
		
        // 定义变量，保存数据
		int b;
		
		// 读取数据
		while((b = fileReader.read()) != -1) {
			System.out.println((char)b); // 每行一个字符
		}
		
		// 关闭资源
		fileReader.close();
	}

}
```

##### 2.2.2.2 使用字符数组读取

```java
import java.io.FileReader;

public class Test3 {
	public static void main(String[] args) throws Exception{
		
		// 存在文件
		// 创建字符输入流对象，关联数据源文件路径
		FileReader fileReader = new FileReader("aaa\\top.txt");
		
        // 定义字符数组，作为装字符数据的容器
		char[] cbuf = new char[2];
		int b;
		
		// 读取数据
		while((b = fileReader.read(cbuf)) != -1) {
			System.out.println(new String(cbuf, 0, b));
		} // 两个字符一行
		
		// 关闭资源
		fileReader.close();
	}

}
```

### 2.3 Writer

java.io类Writer：抽象类，表示用于写出字符流的所有类的超类，将指定的字符信息写出到目的地，定义了一些基本的共性方法

#### 2.3.1 字符输出流的基本方法

```java
void write(char[] cbuf) 
	写入一个字符数组。  
    
abstract void write(char[] cbuf, int off, int len) 
	写入字符数组的一部分。  
    
void write(int c) 
	写一个字符  

void write(String str) 
	写一个字符串  

void write(String str, int off, int len) 
	写一个字符串的一部分。  

abstract void close() 
	关闭流，先刷新。
    
abstract void flush() 
	刷新流。  
```

### 2.4 FileWriter

![](https://github.com/lixingyi123/JavaNotes/blob/main/java-basics/10-IO/images/FileWriter%E7%BB%A7%E6%89%BF%E4%BD%93%E7%B3%BB.png?raw=true)

#### 2.4.1 FileWriter构造方法

```java
FileWriter(File file) 
	给一个File对象构造一个FileWriter对象。
    
FileWriter(File file, boolean append) 
	给一个File对象构造一个FileWriter对象。  

FileWriter(String fileName) 
	构造一个给定文件名的FileWriter对象。  
    
FileWriter(String fileName, boolean append) 
	构造一个FileWriter对象，给出一个带有布尔值的文件名，表示是否附加写入的数据。  
```

创建流对象时，需要传入一个文件路径，当文件路径不存在时，会自动创建txt文件

```java
import java.io.FileWriter;

public class Test3 {
	public static void main(String[] args) throws Exception{
		
		// 文件存在
		FileWriter filewriter = new FileWriter("aaa\\top.txt");
		
		// 文件不存在
		FileWriter fileWriter1 = new FileWriter("aaa\\eee\\top.txt"); 
		
	}

}
```

#### 2.4.2 FileWriter写出数据

##### 2.4.2.1 每次写入单个数据

```java
import java.io.FileWriter;

public class Test3 {
	public static void main(String[] args) throws Exception{
		
		// 文件存在
		FileWriter filewriter = new FileWriter("aaa\\top.txt");
		
		filewriter.write('a');
		filewriter.write('b');
		// ab
		filewriter.close();
	}

}
```

**注意：未调用close（）方法时，数据只是保存到了缓冲区，并未写出到文件中**

##### 2.4.2.2 写入字符数组

```java
import java.io.FileWriter;

public class Test3 {
	public static void main(String[] args) throws Exception{
		
		// 文件存在
		FileWriter filewriter = new FileWriter("aaa\\top.txt");
		
		char[] cbuf = {'a', 'b', 'c', '你', '好'};
		filewriter.write(cbuf);
		filewriter.write(cbuf, 0, 3);
		
		filewriter.close();
	}

}

结果：
    abc你好abc
```

##### 2.4.2.3 写出字符串

```java
import java.io.FileWriter;

public class Test3 {
	public static void main(String[] args) throws Exception{
		
		// 文件存在
		FileWriter filewriter = new FileWriter("aaa\\top.txt");
		
		String msg = "Hello，你好呀！";
		filewriter.write(msg);
		filewriter.write(msg, 0, 3);
		
		filewriter.close();
	}

}

结果：
    Hello，你好呀！Hel
```

##### 2.4.2.4 续写和换行(\r\n)

续写和换行使用**"\r\n"**符号

```java
import java.io.FileWriter;

public class Test3 {
	public static void main(String[] args) throws Exception{
		
		// 文件存在
		FileWriter filewriter = new FileWriter("aaa\\top.txt");
		
		char[] cbuf = {'a', 'b', 'c', 'd'};
		filewriter.write(cbuf);
		filewriter.write("\r\n");// 换行
		filewriter.write(cbuf, 0, 3);
		
		filewriter.close();
	}

}
```

##### 2.4.2.5 flush()和close()

因为内置缓冲区的原因，如果不关闭输出流，是无法写出数据到文件中，但是将流对象关闭之后，无法再继续写出数据。**如果既想写出数据，又想继续使用流，就使用flush方法**，fiush（）过后前面写的数据就已经写入文件了

flush() 方法：**刷新缓冲区**，流对象就可以继续使用

close()方法：关闭流，释放系统资源，关闭前会**刷新缓冲区**

==注意点：只要刷新了缓冲区，数据就写入文件中了==

**即便是flush方法写出了数据，操作的最后还是要调用close方法，释放系统资源。**

```java
import java.io.FileWriter;

public class Test3 {
	public static void main(String[] args) throws Exception{
		
		// 文件存在
		FileWriter filewriter = new FileWriter("aaa\\top.txt");
		
		filewriter.write('刷');
		filewriter.flush();
		filewriter.write('新');
		filewriter.flush();
		
		filewriter.close();
	}

}
```

## 3、属性集

java.util类Properties类，表示一个持久的属性集，它使用键值结构存储数据，每个键机器对应的值都是字符串

### 3.1 构造方法

```java
Properties() 
	创建一个没有默认值的空属性列表。    
```

### 3.2 方法

```java
 Object setProperty(String key, String value) 
     保存一对属性
     
 String getProperty(String key) 
     使用此属性列表中指定的键搜索属性值
     
 Set<String> stringPropertyNames() 
     所有键的名称的集合
```

```java
import java.util.Properties;
import java.util.Set;

public class Test7 {
	public static void main(String[] args) {
		// 创建properties对象
		Properties pro = new Properties();
		
		// 存储键值对
		pro.setProperty("K1", "V1");
		pro.setProperty("K2", "V2");
		pro.setProperty("K3", "V3");
        pro.setProperty("K3", "V3"); // 不会进入
		
		// pro
		Set<String> keys = pro.stringPropertyNames();
		System.out.println(keys);
		
		// 根据键值对查找
		for (String key : keys) {
			String value = pro.getProperty(key);
			System.out.println(key + "=" + value);
		}
	}

}
```

### 3.3 Properties类与流相关的方法

文本中的数据，必须是键值对形式，可以使用空格，**等号**，冒号等分别

```java
void load(InputStream inStream) 
          从输入流中读取属性列表（键和元素对）。 
```

```java
import java.io.FileInputStream;
import java.util.Properties;
import java.util.Set;

public class Test7 {
	public static void main(String[] args) throws Exception{
		// 创建properties对象
		Properties pro = new Properties();
		
		pro.load(new FileInputStream("src\\db.properties"));
		
		Set<String> keys = pro.stringPropertyNames();
		
		// 根据键值对查找
		for (String key : keys) {
			String value = pro.getProperty(key);
			System.out.println(key + "=" + value);
		}
	}

}
```

### 3.4 Properties开发中的使用

1. 开发中配置文件一般是后缀为.properties的文件
2. 开发中的配置文件一般放在src目录下
3. 开发中，配置文件中的内容一般不会出现中文
4. 开发中，一般只会去配置文件中读取数据

```java
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.InputStream;
import java.util.Properties;
import java.util.Set;

public class Test4 {
	public static void main(String[] args) throws Exception{
		// 创建属性集对象
		Properties properties = new Properties();
		
		// 加载文本信息到属性集
		properties.load(new FileInputStream("src\\db.properties"));
        // 了解：直接获取一个流，该流的默认路径就是src
		// InputStream is = Test4.class.getClassLoader().getResourceAsStream("db.properties");
		/// properties.load(is);
		
		// 遍历集合打印
		Set<String> strings = properties.stringPropertyNames();
		for(String key : strings) {
			System.out.println(key + "," + properties.getProperty(key));
		}
		
		
		System.out.println("==============");
		
		// 往properties对象中添加键值对
		properties.setProperty("q", "b");
		
		// 把properties对象中所有的键值对重新写回到db.properties中
		properties.store(new FileOutputStream("src\\db.properties"), "wanhe");
	}
 
}

```

## 4、缓冲流

高效率读写的缓冲流，转换编码的转换流，能够持久化存储对象的序列化流。这些流都是在基本流对象之上创建而来的

**缓冲流也叫高效流**，四个基本流：FileXxxx;

**字节缓冲流：**BufferedInputStream,BufferedOutputStream

**字符缓冲流：**BufferedReader, BufferedWriter

**缓冲流的基本原理：**==在创建流对象时，会创建一个内置的默认大小的缓冲区数组，通过缓冲区读写，减少IO次数，从而提高读写效率==

### 4.1 字节缓冲流

#### 4.1.1 构造方法

```java
BufferedInputStream(InputStream in);
	创建一个新的缓冲输入流
        
BufferedOutputStream(OutputStream out);
	创建一个新的缓冲输出流
```

```java
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.BufferedInputStream;
import java.io.BufferedOutputStream;

public class Test5 {
	public static void main(String[] args) throws Exception{
		long start = System.currentTimeMillis();
		
		// 创建字节输入流
		FileInputStream fis = new FileInputStream("aaa\\jdk17.exe");
		// 字节输入缓冲流
		BufferedInputStream bis = new BufferedInputStream(fis);
		
		// 创建字节输出流
		FileOutputStream fos = new FileOutputStream("aaa\\eee\\jdk17Copy.exe");
		// 创建字节输出缓冲区
		BufferedOutputStream bos = new BufferedOutputStream(fos);
		
		int len;
		
		while((len = bis.read()) != -1) {
			bos.write(len);
		}
		
		fos.close();
		fis.close();
		
		long end = System.currentTimeMillis();
		
		System.out.println("复制该文件总共花了：" + (end - start) + "ms");
	}

}

有点慢
```

#### 4.1.2 字节数组型（读写数据）

```java
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.BufferedInputStream;
import java.io.BufferedOutputStream;

public class Test5 {
	public static void main(String[] args) throws Exception{
		long start = System.currentTimeMillis();
		
		// 创建字节输入流
		FileInputStream fis = new FileInputStream("aaa\\jdk17.exe");
		// 字节输入缓冲流
		BufferedInputStream bis = new BufferedInputStream(fis);
		
		// 创建字节输出流
		FileOutputStream fos = new FileOutputStream("aaa\\eee\\jdk17Copy.exe");
		// 创建字节输出缓冲区
		BufferedOutputStream bos = new BufferedOutputStream(fos);
		
		byte[] byte1 = new byte[8154];
		int len;
		
		while((len = bis.read(byte1)) != -1) {
			bos.write(byte1, 0, len);
		}
		
		fos.close();
		fis.close();
		
		long end = System.currentTimeMillis();
		
		System.out.println("复制该文件总共花了：" + (end - start) + "ms");
	}

}

结果：
    复制该文件总共花了：282ms
    结果很快
```

### 4.2 字符缓冲流

```java
BufferedReader(Reader in)
    创建一个字符缓冲输入流

BufferedWriter(Writer out)
    创建一个字符缓冲输出流
```

#### 4.2.1 读数据

```java
import java.io.BufferedReader;
import java.io.FileReader;

public class Test6 {
	public static void main(String[] args) throws Exception{
		// 读
		FileReader file = new FileReader("aaa\\top.txt");
		
		BufferedReader br = new BufferedReader(file);
		
		String line;
		// readLine()读一行文字
		// newLine()写一行文字
		while((line = br.readLine()) != null) {
			System.out.println(line);
		}
		
		br.close();
	}

}
```

#### 4.2.2 写数据

```java
import java.io.FileWriter;
import java.io.BufferedWriter;

public class Test6 {
	public static void main(String[] args) throws Exception{
		
		FileWriter fw = new FileWriter("aaa\\top.txt");
		BufferedWriter bw = new BufferedWriter(fw);
		
		bw.write("静夜思");
		bw.newLine();
		
		bw.write("床前明月光");
		bw.newLine();
		
		fw.close();
	}
}
```

## 5、转换流

### 5.1 字符编码

#### 5.1.1 字符编码发展历程

```java
阶段1:
计算机只认识数字,我们在计算机里一切数据都是以数字来表示,因为英文符号有限,
所以规定使用的字节的最高位是0.每一个字节都是以0~127之间的数字来表示,比如A对应65,a对应97.
这就是美国标准信息交换码-ASCII.

阶段2:
随着计算机在全球的普及,很多国家和地区都把自己的字符引入了计算机,比如汉字.
此时发现一个字节能表示数字范围太小,不能包含所有的中文汉字,那么就规定使用两个字节来表示一个汉字.
规定:原有的ASCII字符的编码保持不变,仍然使用一个字节表示,为了区别一个中文字符与两个ASCII码字符,
中文字符的每个字节最高位规定为1(中文的二进制是负数).这个规范就是GB2312编码,
后来在GB2312的基础上增加了更多的中文字符,比如汉字,也就出现了GBK.

阶段3:
新的问题,在中国是认识汉字的,但是如果把汉字传递给其他国家,该国家的码表中没有收录汉字,其实就显示另一个符号或者乱码.
为了解决各个国家因为本地化字符编码带来的影响,咱们就把全世界所有的符号统一进行编码-Unicode编码.
此时某一个字符在全世界任何地方都是固定的,比如’哥’,在任何地方都是以十六进制的54E5来表示.
Unicode的编码字符都占有2个字节大小.

常见的字符集:
ASCII: 占一个字节,只能包含128个符号. 不能表示汉字
ISO-8859-1:(latin-1):占一个字节,收录西欧语言,.不能表示汉字.
ANSI:占两个字节,在简体中文的操作系统中 ANSI 就指的是 GB2312.
GB2312/GBK/GB18030:占两个字节,支持中文.
UTF-8:是一种针对Unicode的可变长度字符编码，又称万国码,是Unicode的实现方式之一。
编码中的第一个字节仍与ASCII兼容，这使得原来处理ASCII字符的软件无须或只须做少部份修改，即可继续使用。
因此，它逐渐成为电子邮件、网页及其他存储或传送文字的应用中，优先采用的编码。互联网工程工作小组（IETF）要求所有互联网协议都必须支持UTF-8编码。

UTF-8 BOM:是MS搞出来的编码,默认占3个字节

存储字母,数字和汉字:
存储字母和数字无论是什么字符集都占1个字节.


不能使用单字节的字符集(ASCII/ISO-8859-1)来存储中文.

-字符的编码和解码操作:
编码: 把字符串转换为byte数组.
解码: 把byte数组转换为字符串.
一定要保证编码和解码的字符相同,否则乱码.
```

### 5.2 字符编码速记

1. GBK家族占两个字节，UTF-8家族占3个字节
2. 互联网工作小组要求所有互联网协议都必须支持UTF-8编码
3. 在GB2312的基础上增加了更多的中文字符，比如汉字，也就出现了GBK
4. UTF-8是一种针对Unicode的可变长度字符编码，又称万国码，是Unicode的实现方式之一

### 5.3 InputStreamReader

InputStreamReader是reader的子类，它的字符集可以由名称指定，也可以接收平台默认的字符集

#### 5.3.1 构造方法

```java
InputStreamReader(InputStream in)
    创建一个使用默认字符集的InputStreamReader

InputStreamReader(InputStream in, String charseName)
    创建使用指定字符集的InputStreamReader
```

```java
public class Test{
    public static void main(String[] args) throws Exception{
        // 文件路径
        String filename = "aaa\\eee\\a.txt";
        
        // 创建流对象，默认UTF-8
        InputStreamReader isr = new InputStreamReader(new FileInputStream(filename));
        
        // 创建流对象，使用GBK
        InputStreamReader isr2 = new InputStreamReader(new FileInputStream(filename), "GBK");
        
        int read;
        while ((read == isr.read()) != -1){
            System.out.println((char)read);
        }
        isr.close();
    }
}
```

### 5.4 OutputStreamWriter

```java
OutputStreamWriter(OutputStream out)
    创建使用默认字符编码的OutputStreamWriter
    
OutputStreamWriter(OutputStream out, String charseName)
    创建使用指定的字符编码的OutputStreamWriter
```

```java
public class Test{
    public static void main(String[] args) throws Exception{
        // 文件路径
        String filename = "aaa\\eee\\b.txt";
        // 创建流对象，默认UTF8编码
        OutputStreamWriter osw = new OutputStreamWriter(new FileOutputStream(filename));
        osw.write("你好");
        osw.close();
        
        // 创建流对象
        OutputStreamWriter osw2 = new OutputStreamWriter(new FileOutputStream(filename), "GBK");
        osw2.write("你好");
        osw2.close();
    }
}
```

### 5.5 转换文件编码

将GBK编码的文件，转换为UTF-8编码的文件

```java
public class Test{
    public static void main(String[] args){
        // 将gbk编码的文件转换为UTF-8编码的文件
        FileInputStream fis = new FileInputStream("aaa\\jbk.txt");
        InputStreamReader isr = new InputStreamReader(fis, "GBK");
        
        FileOutputStream fos = new FileOutputStream("aaa\\a.txt");
        OutputStreamWriter osw = new OutputStreamWriter(fos, "UTF-8");
        
        int len;
         while ((len == isr.read() != -1){
             osw.write(len);
         }
         osw.close();
         isr.close();
    }
}
```

## 6、序列化

Java提供了一种对象序列的机制，用一个字节码可以表示一个对象，该字节序列里面包含对象的数据，类型，存储的属性等。等字节序列写出到文本之后，相当于持久保存了一个对象信息。

同样，该字节序列还可以从文件中读取出来，称为反序列化

### 6.1 ObjectOutputStream

将Java对象的基本数据类型写出到文件，实现对象的持久存储

```java
ObjectOutputStream(OutputStream out)
    创建写入指定OutputStream的ObjectOutputStream
```

ObjectOutputStream序列化操作：

**该类必须实现Serializable接口**

```java
public class Test{
    // 忽略警告
    @SuppressWarnings("resource")
    public static void main(String[] args){
        Student stu = new Student("张三", 19);
        stu.anl = new Animal();
        
        
        // 创建序列化流对象，关联本地的文件路径
        FileOutputStream fos = new FileOutputStream("aaa\\eee\\a.txt");
        
        ObjectOutputStream oos = new ObjectOutputStream(fos);
        
        // 写出对象
        oos.writeObject(stu);
       
        // 关闭流
        oos.close();
    }
    
}
```

### 6.2 反序列化

```java
punlic class Test{
    public static void main(String[] args) throws Excepton{
        // 创建序列化流对象
        ObjectInputStream ois = new ObjectInputStream(new FileInputStream("aaa\\eee\\b.txt");
       	
        Student stu = (Student)ois.readObject(); 
        System.out.println(stu);
    	
        ois.close();
    }
}
```

### 6.3 打印流

```java
public class Test{
    public static void main(String[] args) throws Exception{
        // 打印流对象
        PrintStream ps = new PrintStream("aaa\\a.txt");
        
        // 打印数据
        ps.print(97);
        ps.print('a');
        ps.print("你好");
        
        // 关闭流
        ps.close();
    }
}
```

## 7、commons-io工具包

**commons-io：是一组有关IO的类库，可以提高IO功能开发的效率**

==使用步骤：==

1. 下载jar包，[Commons IO官网](https://commons.apache.org/proper/commons-io/)
2. 在eclipse中新建lib文件，文件与scr并列，并把jar包复制到lib中
3. 选择jar包，右击：Build path-->Add to Build Path，在目录中就会多出一个文件

```java
import java.io.File;

import org.apache.commons.io.FileUtils;

public class Test{
    public static void main(String[] args) throws Exception{
        File f1 = new File("ddd");
        File f2 = new File("ccc");
        
        // f1中的整个文件全部被拷贝进bbb中
        FileUtils.copyDirectoryToDirectory(f1, f2);
    }
}
```

## 8、Junit单元测试

**概述：**Junit是Java语言编写的第三方的测试框架（工具类）

**作用：用来做单元测试——测试某个普通方法**，可以像main方法一样独立运行，专门用来测试某个方法

```java
public class Test01 {
	public static void main(String[] args) throws Exception{
	}
	
	@Test
	public void show1() {
		System.out.println("show1方法开始执行");
	}
	@Test
	public void show2() {
		System.out.println("show2方法开始执行");
	}
}
```

**注意事项：**

1. 用Junit测试方法时**权限修饰符一定是public**，会报错
2. 用Junit测试方法，方法的**返回值类型一定是void**，不然会报错
3. 用Junit测试方法，**方法不能有参数**，会报错
4. **测试方法的声明之上一定要加@Test注解**

```java
import org.junit.AfterClass;
import org.junit.Before;
import org.junit.BeforeClass;
import org.junit.Test;


public class Test01 {
	@Test
	public void show2() {
		System.out.println("show2方法开始执行");
	}
	
	// 会在所有测试方法之前执行一次，而且只执行一次
	@BeforeClass
	public static void show1() {
		System.out.println("show1方法开始执行");
	}
	
	// 会在所有测试方法之后执行一次，而且只执行一次
	@AfterClass
	public static void show4() {
		System.out.println("show4方法开始执行");
	}
	
	@Test
	public void show3() {
		System.out.println("show3方法开始执行");
	}
	
	// 该方法会在每一个测试方法之前执行一次
	@Before
	public void show5() {
		System.out.println("show5方法开始执行");
	}

}

结果：
show1方法开始执行
show5方法开始执行
show2方法开始执行
show5方法开始执行
show3方法开始执行
show4方法开始执行
```
