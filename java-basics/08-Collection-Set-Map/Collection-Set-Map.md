<p align = "center" ><font size = 6， color = "#009999">Collectoin & Set & Map</font></p>

## 1、Collection

### 1.1 集合概述

将一系列相同类型的数据聚集在一起，类似于数组

集合不是一个具体的类，而是一系列相同作用的类

### 1.2 单列集合常用类的继承体系

![](https://github.com/lixingyi123/JavaNotes/blob/main/java-basics/08-Collection-Set-Map/images/%E9%9B%86%E5%90%88%E4%BD%93%E7%B3%BB.png?raw=true)

```java
Collection集合：是一个接口，所有单列集合的顶层父接口，该集合中的所有方法可以被所有单列集合共享
    List:接口，父类可以重复，元素有索引，元素存取有序
        ArrayList集合：实现类，查询快，增删慢
        LinkedList集合：实现类，查询慢，增删快
       
    Set：接口，元素不可重复（唯一），元素无索引
        HashSet集合：实现类，元素存取无序
        LinkedHashSet集合：实现类，元素存取有序
        TreeSet集合：实现类，可以对元素进行排序      
```

Collection是所有单列集合的父接口，因此在此接口中定义的通用方法在所有单列集合类中都可使用

### 1.3 Collection通用方法

```java
boolean add(E e)
    确保此collection包含指定的元素
    
boolean contains(Object o) 
	如果此集合包含指定的元素，则返回 true 。  
    
boolean equals(Object o) 
	将指定的对象与此集合进行比较以获得相等性。 
    
boolean isEmpty() 
	如果此集合不包含元素，则返回 true 。
    
boolean remove(Object o) 
	从该集合中删除指定元素的单个实例（如果存在）（可选操作）。 
    
int size() 
	返回此集合中的元素数。 
    
Object[] toArray() 
	返回一个包含此集合中所有元素的数组。 
    
void clear()
    从此集合中删除所有元素（可选操作）。 此方法返回后，集合将为空。 
```

```java
import java.util.Collection;
import java.util.ArrayList;
import java.util.Arrays;

public class Test{
    public static void main(String[] args){
        Collection<String> list = new ArrayList<String>();
        
        // add
        list.add("Hello");
        list.add("Hi");
        list.add("你好");
        
        System.out.println(list); // [Hello, Hi, 你好]
        
        // 清空集合中的所有元素
        // list.clear();
        // System.out.println(list); // []
        
        // 查询list的的个数
        System.out.println(list.size()); // 3
        
        // 删除列表中的第二个元素
        list.remove("Hi");
        System.out.println(list); // [Hello, 你好]
        
        // 判断集合中是否包含某个元素
        System.out.println(list.contains("Hi")); // false
        
        // 判断集合是否为空
        System.out.println(list.isEmpty()); // false
        
        // 返回一个包含此集合中所有元素的数组。
        Object[] array = list.toArray();
        System.out.println(Arrays.toString(array)); // [Hello, 你好]
        
    }
}
```

## 2、迭代器（Iterator）

在程序的开发中，**经常需要遍历单列集合中的所有元素**，针对这种需求，JDK专门提供了一个java.util接口 **Iterator<E>**

### 2.1 迭代的概念

迭代：**Collection集合元素的通用获取方式，在取元素之前先判断集合中有没有元素，如果有元素，就把这个元素取出来，继续再判断，如果还有就再取出，直到把集合中的元素全部取出为止。**这种方式专业术语叫做迭代。

#### 2.1.1 迭代的获取方式

```java
Iterator<E> iterator()
    返回在此collection的元素上进行迭代的迭代器
    
boolean hasNext()
    如果有元素，就返回true
    
E next()
    返回迭代的下一个元素
    
void remove()
    从迭代器指向的collection中移除迭代器返回的最后一个元素
```

```java
import java.util.Collection;
import java.util.ArrayList;
import java.util.Iterator;

public class Test{
    public static void main(String[] args){
        Collection<String> col = new ArrayList<String>();
        
        col.add("123");
        col.add("abc");
        col.add("123");
        
        // 获取迭代器对象
        Iterator<String> it = col.iterator();
        
        // 循环判断集合中是否有元素可以迭代
        while (it.hasNext()){
            // 可以迭代就进行操作
            String e = it.next();
            System.out.println(e);  
        }
    }
}
```

### 2.2 迭代器的问题

#### 2.2.1 问题一

```java
import java.util.Collection;
import java.util.ArrayList;
import java.util.Iterator;

public class Test{
    public static void main(String[] args){
        Collection<String> col = new ArrayList<String>();
        
        col.add("123");
        col.add("abc");
        col.add("123");
        
        // 获取迭代器对象
        Iterator<String> it = col.iterator();
        
        // 循环判断集合中是否有元素可以迭代
        while (it.hasNext()){
            // 可以迭代就进行操作
            String e = it.next();
            System.out.println(e);  
        }
        
        // 问题1：
        // 再获取集合中的元素就会出现异常
        // String next = it.next(); // java.util.NoSuchElementException
        // System.out.println(next);
        
        // 如果迭代完了，还想重新迭代元素，就需要重新获取一个迭代器
    }
}
```

#### 2.2.2 问题二

**在迭代器循环遍历过程中不能增删元素**，否则会报：java.util.ConcurrentModificationException错误

```java
import java.util.Collection;
import java.util.ArrayList;
import java.util.Iterator;

public class Test{
    public static void main(String[] args){
        Collection<String> col = new ArrayList<String>();
        
        col.add("123");
        col.add("abc");
        col.add("123");
        
        // 获取迭代器对象
        Iterator<String> it = col.iterator();
        
        // 循环判断集合中是否有元素可以迭代
        while (it.hasNext()){
            // 可以迭代就进行操作
            String e = it.next();
            // col.add("12334"); // 报错
            // col.remove("123");// 报错
            System.out.println(e);  
        }
      
    }
}
```

### 2.3 for-each循环

**专门用来遍历数组和集合的，内部原理就是迭代器，所以只能遍历元素，不能对数据进行增删操作**

格式：

```java
for (数据类型 变量名: Collection集合或者数组){
    // 操作代码
}
```

## 3、List接口

**ArrayList的增删慢，查找快**

**LinkedList的增删快，查找慢**

### 3.1 LinkedList

#### 3.1.1 常用方法

```java
void addFirst(E e)
    将指定元素插入此列表的开头
    
void addLast(E e)
    将指定元素添加到此列表的末尾
    
E getFirst() 
    返回此列表的第一个元素。 
    
E getLast() 
    返回此列表的最后一个元素。 
    
E removeFirst() 
    移除并返回此列表的第一个元素。 
    
E removeLast() 
    移除并返回此列表的最后一个元素。 
```

```java
import java.util.LinkedList;

public class Test{
    public static void main(String[] args){
        // 创建LinkedList对象
        LinkedList<String> list = new LinkedList<String>();
        
        // 添加元素
        list.add("123");
        list.add("abc");
        list.add("123");
        System.out.println(list); // [123, abc, 123]
        
        // 首位添加元素
        list.addFirst("ABC");
        list.addLast("abc");
        System.out.println(list); // [ABC, 123, abc, 123, abc]
        
        // 获取首尾元素
        System.out.println(list.getFirst()); // ABC
        System.out.println(list.getLast()); // abc
        
        // 移除首尾元素
        list.removeFirst();
        System.out.println(list); // [123, abc, 123, abc]
        
        list.removeLast();
        System.out.println(list); // [123, abc, 123]       
    }
}
```

## 4、Collections类

**Collections类是一个集合工具类，用来对集合进行操作**

方法：

```java
static void shuffle(List<?> list) 
	使用默认的随机源随机排列指定的列表。  
    
static <T extends Comparable<? super T>>
void sort(List<T> list) 
	根据其元素的natural ordering对指定的列表进行排序。  
```

```java
import java.util.ArrayList;
import java.util.Collections;

public class Test{
    public static void main(String[] args){
        ArrayList<Integer> list = new ArrayList<Integer>();
        
        list.add(300);
		list.add(100);
		list.add(200);
		list.add(500);
		list.add(400);
        
        System.out.println(list); // [300, 100, 200, 500, 400]
        
        Collections.shuffle(list);   
        System.out.println(list); // [200, 300, 400, 500, 100]
                
        Collections.sort(list);
        System.out.println(list); // [100, 200, 300, 400, 500]
    }
}
```

## 5、可变参数

如果定义一个方法，需要接收多个参数，多个参数类型保持一致

格式：

```java
修饰符 返回值类型 方法名（参数类型...形参名）;
```

```java
public class Test{
    public static void main(String[] args){
        method1(1, 2, 3, 4, 5);
        method2(1, 2, 3, 4, 5);
    }
    
    public static void method1(int num1, int num2, int num3, int num4, int num5){
        
    }
    
    public static void method2(int... nums){
        
    }
}
```

### 5.1 注意事项

1. 一个方法只能有一个可变参数
2. 如果方法中有多个参数，可变参数放在最后

## 6、Set接口

### 6.1 Set接口的概述

1. **Set继承于Collection接口**，是一个**不允许出现重复元素**， 更正式地，集合不包含一对元素`e1`和`e2`  ，使得`e1.equals(e2)` ，并且最多一个空元素。
2. **Set中的元素无索引**，所以遍历元素的方式就只有：**增强for循环，或者迭代器**

#### 6.1.1 Set接口的分类

1. ==HashSet==：实现类，元素存取无序
2. ==LinkedList==：实现类，元素存取有序
3. ==TreeSet==：实现类，可以对元素进行排序

![](https://github.com/lixingyi123/JavaNotes/blob/main/java-basics/08-Collection-Set-Map/images/Set%E6%A1%86%E6%9E%B6.png?raw=true)

### 6.2 HashSet

HashSet是Set接口的一个具体实现类，元素不可重复，无序

```java
import java.util.HashSet;
import java.util.Iterator;

public class Test {
	public static void main(String[] args) {
		// 创建HashSet对象
		HashSet<String> set = new HashSet<String>();
		
		// 添加元素
		set.add("abc");
		set.add("123");
		set.add("");
		set.add("Hello");
		set.add("你好");
		
		System.out.println(set); // [, 123, abc, Hello, 你好]，无序
		
		// for-each遍历
		for (String s : set) {
			System.out.println(s);
		}
		
		// 迭代器遍历
		Iterator<String> it = set.iterator();
		while (it.hasNext()) {
			System.out.println(it.next());
		}
	}

}
```

### 6.3 LinkedHashSet

**特点：元素存取有序**

```java
public class LinkedHashSet<E> extends HashSet<E> implements Set<E>
```

```java
import java.util.LinkedHashSet;
import java.util.Iterator;

public class LinkedTest {
	public static void main(String[] args) {
		// 创建LinkedHashSet对象
		LinkedHashSet<Integer> set = new LinkedHashSet<Integer>();
		
		// 添加元素
		set.add(500);
		set.add(400);
		set.add(344);
		set.add(98);
		set.add(888);
		System.out.println(set); // [500, 400, 344, 98, 888]有序
		
		// for-each遍历
		for (int s : set) {
			System.out.println(s);
		}
		
		// Iterator遍历
		Iterator<Integer> it = set.iterator();
		while (it.hasNext()) {
			System.out.println(it.next());
		}
		
	}

}
```

### 6.4 TreeSet

TreeSet集合是Set接口的一个实现类

**特点：元素唯一，元素无索引，可以对元素进行排序**

```java
Iterator<E> descendingIterator() 
	以降序返回该集合中的元素的迭代器。  
    
Iterator<E> Iterator()
    以升序返回该集合的元素的迭代器
```

```java
import java.util.TreeSet;
import java.util.Iterator;

public class TreeTest {
	public static void main(String[] args) {
		// 创建TreeSet对象
		TreeSet<Integer> set = new TreeSet<Integer>();
		
		// 添加元素
		set.add(500);
		set.add(999);
		set.add(600);
		set.add(888);
		set.add(100);
		
		System.out.println(set); // [100, 500, 600, 888, 999]自动排序
		
		// for-each遍历
		for (int s : set) {
			System.out.println(s);
		}
		
		// 迭代器遍历
		// 降序
		Iterator<Integer> it = set.descendingIterator();
		while (it.hasNext()) {
			System.out.print(it.next() + " "); // 999 888 600 500 100 
		}		
	}
}
```

## 7、Map

```java
Interface Map<K,V>， K用来限制键的类型，V用来限制值的类型
```

### 7.1 Map的特点

1. Map集合以键值对的形式存储元素
2. Map集合中的键是唯一的，值可以重复，如果键重复了，那么值就会被覆盖

![](https://github.com/lixingyi123/JavaNotes/blob/main/java-basics/08-Collection-Set-Map/images/Map%E7%BB%A7%E6%89%BF%E4%BD%93%E7%B3%BB.png?raw=true)

### 7.2 Map常用方法

```java
V put(K key, V value) 
    将指定的值与此映射中的指定键关联（可选操作）。 
    
V remove(Object key) 
    如果存在一个键的映射关系，则将其从此映射中移除（可选操作）。
    
V get(Object key) 
    返回指定键所映射的值；如果此映射不包含该键的映射关系，则返回 null。
    
boolean containsKey(Object key) 
    如果此映射包含指定键的映射关系，则返回 true。
    
Set<K> keySet() 
    返回此映射中包含的键的 Set 视图。 
    
Collection<V> values() 
    返回此映射中包含的值的 Collection 视图。 
    
Set<Map.Entry<K,V>> entrySet() 
	返回此地图中包含的映射的Set视图。  
    
boolean isEmpty() 
	如果此地图不包含键值映射，则返回 true 。 
    
int size() 
	返回此地图中键值映射的数量。  
```

```java
import java.util.Collection;
import java.util.HashMap;
import java.util.Map;
import java.util.Set;

public class HashTest {
	public static void main(String[] args) {
		// 创建HashMap对象
		HashMap<String, Integer> map = new HashMap<String, Integer>();
		
		// 添加元素
		map.put("李四", 18);
		map.put("王五", 30);
		map.put("张三", 24);
		map.put("周六", 70);
		
		System.out.println(map); // {李四=18, 张三=24, 王五=30, 周六=70}
		
		// Map集合键唯一,如果键重复了，值会覆盖
		map.put("张三", 25);
		System.out.println(map); // {李四=18, 张三=25, 王五=30, 周六=70}
		
		// Map的值可以重复
		map.put("张四", 70);
		System.out.println(map); // {张四=70, 李四=18, 张三=25, 王五=30, 周六=70}
		
		// 删除张四这个键对应的键值对
		int v1 = map.remove("张四");
		System.out.println(v1); // 70
		System.out.println(map); // {李四=18, 张三=25, 王五=30, 周六=70}
		
		// 判断此映射是否包含指定键/值的映射关系
		System.out.println(map.containsKey("周六")); // true
		System.out.println(map.containsValue(50)); // false
		
		
		// 获取所有的键
		Set<String> keys = map.keySet();
		System.out.println(keys); // [李四, 张三, 王五, 周六]
		
		// 获取所有的值
		Collection<Integer> values = map.values();
		System.out.println(values); // [18, 25, 30, 70]
		
		// 获取Map中所有键值对
		Set<Map.Entry<String, Integer>> set = map.entrySet();
		System.out.println(set); // [李四=18, 张三=25, 王五=30, 周六=70]
	}

}
```

### 7.3 Map的遍历

#### 7.3.1 键值对方式

```java
import java.util.HashMap;
import java.util.Set;

public class HashTest {
	public static void main(String[] args) {
		// 创建HashMap对象
		HashMap<String, Integer> map = new HashMap<String, Integer>();
		
		// 添加元素
		map.put("李四", 18);
		map.put("王五", 30);
		map.put("张三", 24);
		map.put("周六", 70);
		
		System.out.println(map); // {李四=18, 张三=24, 王五=30, 周六=70}
        
        // 遍历Map
        // 1. 首先获取键
        Set<String> keys = map.keySet();
        // 2. 遍历
        for (String key : keys){
            int value = map.get(key);
            System.out.println("键：" + key + " 值：" + value)：
        }
    }
}
```

### 7.4 HashMap存储自定义类型

当给HashMap中存放自定义对象时，如果自定的对象作为键存在，要保证对象唯一，要重写HashCode（）与equals（）

```java
// Student类
public class Student{
    private String name;
    private int age;
    
    public Student(){
        
    }
    
    public Student(String name, int age){
        this.name = name;
        this.age = age;
    }
    
    public String toString(){
        return "[姓名是：" + this.name + " 年龄是：" + this.age + "]";
    }
}
```

```java
// Test测试类
public class Test{
    public static void main(String[] args){
        // 创建HashMap对象,指定键的类型是Student，值的类型为String
        HashMap<Student, String> map = new HashMap<Student, String>();
        
        Student stu1 = new Student("张三", 18);
        Student stu2 = new Student("李四", 20);
        Student stu3 = new Student("王五", 34);
        Student stu4 = new Student("小六", 9);
        
        // 把学生作为对象存入键，地址作为值，存到map中
        map.put(stu1, "北京");
        map.put(stu2, "上海");
        map.put(stu3, "广州");
        map.put(stu4, "深圳");
        
        System.out.println(map);
        // // {[姓名是：王五 年龄是：34]=广州, [姓名是：张三 年龄是：18]=北京, [姓名是：李四 年龄是：20]=上海, [姓名是：小六 年龄是：9]=深圳}
        
    }

}
```

### 7.5 LinkedHashMap

1. 保证元素的存取顺序一致

2. 保证键的唯一，不重复，否则覆盖

```java
import java.util.LinkedHashMap;

public class LinkedTest {
	public static void main(String[] args) {
		// 创建LinkedList对象
		LinkedHashMap<String, Integer> map = new LinkedHashMap<>();
		
        // 添加元素
		map.put("张三", 19);
		map.put("老刘", 40);
		map.put("二傻", 30);
		map.put("呆子", 20);
		
		System.out.println(map); // {张三=19, 老刘=40, 二傻=30, 呆子=20}	
	}
}
```

### 7.6 TreeMap

可以对元素的键进行排序，**排序的方式有：自然排序与比较器排序**

```java
import java.util.TreeMap;

public class LinkedTest {
	public static void main(String[] args) {
		// 创建LinkedList对象
		TreeMap<Integer, String> map = new TreeMap<>();
		
		map.put(19, "张三");
		map.put(40, "老刘");
		map.put(30, "二傻");
		map.put(20, "呆子");
		
		System.out.println(map); // {19=张三, 20=呆子, 30=二傻, 40=老刘}
		
	}
}
```

## 8、集合的嵌套

### 8.1 List嵌套List

注意：嵌套的两个list必须是相同类型

```java
import java.util.ArrayList;
import java.util.List;

public class Test {
	public static void main(String[] args) {
		ArrayList<String> list1 = new ArrayList<String>();
		
		list1.add("张三");
		list1.add("李四");
		list1.add("王五");
		
		ArrayList<String> list2 = new ArrayList<String>();
		list2.add("小呆");
		list2.add("二傻");
		
		ArrayList<List<String>> list = new ArrayList<List<String>>();
		list.add(list1);
		list.add(list2);
		
		//遍历
		for(List<String> e : list) {//list1 list2
			for(String name : e) {
				System.out.println(name);
			}
		}
	}
}

结果：
张三
李四
王五
小呆
二傻
```

### 8.2 List嵌套Map

```java
import java.util.HashMap;
import java.util.Map;
import java.util.ArrayList;
import java.util.Set;

public class LinkedTest {
	public static void main(String[] args) {
		HashMap<String, Integer> map1 = new HashMap<>();
		map1.put("张三", 19);
		map1.put("老刘", 40);
		map1.put("二傻", 30);
		map1.put("呆子", 20);
		
		HashMap<String, Integer> map2 = new HashMap<>();
		map2.put("二傻", 34);
		map2.put("呆子", 24);
		
		ArrayList<Map<String, Integer>> list = new ArrayList<Map<String, Integer>>();
		list.add(map1);
		list.add(map2);
		
		//遍历
		for(Map<String, Integer> map : list) {//map1 map2
			Set<String> keys = map.keySet();
			for(String key : keys) {
				int age = map.get(key);
				System.out.println("姓名是：" + key + " 年龄是：" + age);
			}
		}
	}
}

结果：
姓名是：呆子 年龄是：20
姓名是：张三 年龄是：19
姓名是：二傻 年龄是：30
姓名是：老刘 年龄是：40
姓名是：呆子 年龄是：24
姓名是：二傻 年龄是：34
```

### 8.3 Map嵌套Map

```java
import java.util.HashMap;
import java.util.Map;
import java.util.Set;

public class LinkedTest {
	public static void main(String[] args) {
		HashMap<String, Integer> map1 = new HashMap<>();
		
		map1.put("张三", 19);
		map1.put("老刘", 40);
		map1.put("二傻", 30);
		map1.put("呆子", 20);
		
		HashMap<String, Integer> map2 = new HashMap<>();
		map2.put("二傻", 34);
		map2.put("呆子", 24);
		
		HashMap<Map<String, Integer>, String> list = new HashMap<Map<String, Integer>, String>();
		list.put(map1, "开发部");
		list.put(map2, "销售部");
		
		//遍历
		Set<Map<String, Integer>> sets = list.keySet();
		for(Map<String, Integer> set : sets) {//map1 map2
			String value = list.get(set);
			Set<String> keySet = set.keySet();
			for(String k : keySet) {
				int v = set.get(k);
				System.out.println("姓名：" + k + ", 年龄：" + v + ", 部门：" + value);
			}
			
			
		}
	}

}

结果：
姓名：呆子, 年龄：20, 部门：开发部
姓名：张三, 年龄：19, 部门：开发部
姓名：二傻, 年龄：30, 部门：开发部
姓名：老刘, 年龄：40, 部门：开发部
姓名：呆子, 年龄：24, 部门：销售部
姓名：二傻, 年龄：34, 部门：销售部
```



## 9、Swing

概述：Swing是jdk提供的一系列的类

这些类是用于构建图形化界面的

### 9.1 Swing的安装步骤

1. 安装插件，不要解压，也可以去[eclipse官网](https://www.eclipse.org/windowbuilder/download.php)复制链接
2. 在eclipse中安装插件或则粘贴链接地址进行安装

help--install new software

![](https://github.com/lixingyi123/JavaNotes/blob/main/java-basics/08-Collection-Set-Map/images/swing1.png?raw=true)

![](https://github.com/lixingyi123/JavaNotes/blob/main/java-basics/08-Collection-Set-Map/images/swing2.png?raw=true)

![](https://github.com/lixingyi123/JavaNotes/blob/main/java-basics/08-Collection-Set-Map/images/swing3.png?raw=true)

3. 一直点next

   1.最后一步遇到一个协议，选中同意，完成安装

   2.点击完成后，在eclipse的右下角会出现安装读条

   3.安装完成后，会弹出提示框，提示重启eclipse，选择**【restart】**

   4.重启之后，在指定的包上面选择--->other---->Jframe