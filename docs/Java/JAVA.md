---
title: JAVA
createTime: 2025/07/08 17:03:15
permalink: /article/jb4gkgx6/
---
# JAVA
## IDEA快捷键

| 快捷键               | 作用                     |
| -------------------- | ------------------------ |
| ctrl + alt + t       | 生成包裹代码块(if/for)   |
| alt + insert         | 自动生成类函数           |
| ctrl + alt + v       | 自动生成变量类型和变量名 |
| ctrl + b             | 查看源码                 |
| alt + enter          | 查看 idea 的提示，导包   |
| (alt+ 鼠标左键)/中键 | 多行编辑                 |

## 基础

### 数据类型

- 基本数据类型：整数类型（byte、short、int、long）、浮点类型（float、double）、字符类型（char）、布尔类型（boolean）
- 引用数据类型：类、接口、数组

### 运算符

- 算术运算符：+、-、*、/、%（取余）、++、--
- 关系运算符：==、!=、>、<、>=、<=
- 逻辑运算符：&&（与）、||（或）、！（非）
- 赋值运算符：=、+=、-=、*=、/=、%=、&=、|=、^=、<<=、>>=、>>>=
- 条件运算符：?:
- 位运算符：&（按位与）、|（按位或）、^（按位异或）、~（按位取反）、<<（左移）、>>（右移）、>>>（无符号右移）

### 数组

##### 声明

`int[] arr = new int[5];`



## 数据结构

### 包装类

基本数据类型对应的包装类：

- byte、short、int、long：Byte、Short、Integer、Long
- float、double：Float、Double
- char：Character
- boolean：Boolean

#### Integer/Long

- `Integer.parseInt(String s)`: 将字符串解析为十进制整数。
- `Integer.toBinaryString(int i)`: 将整数转换为二进制字符串。
- `Integer.toHexString(int i)`: 将整数转换为十六进制字符串。
- `Integer.toOctalString(int i)`: 将整数转换为八进制字符串。
- `Integer.valueOf(String s)`: 将字符串参数解析为带符号的十进制整数，并返回一个 `Integer` 实例。
- `Integer.valueOf(int i)`: 返回一个表示指定整数的 `Integer` 实例。

#### Float/Double

- `Float.parseFloat(String s)`: 将字符串解析为浮点数。
- `Float.toHexString(float f)`: 将浮点数转换为十六进制字符串。
- `Float.isNaN(float v)`: 检查指定的浮点数是否为 NaN（非数字）。
- `Float.isInfinite(float v)`: 检查指定的浮点数是否为无穷大。
- `Float.valueOf(String s)`: 将字符串参数解析为浮点数，并返回一个 `Float` 实例。
- `Float.valueOf(float f)`: 返回一个表示指定浮点数的 `Float` 实例。

#### Short/Byte/Boolean

- `Short.parseShort(String s)`: 将字符串解析为短整型。
- `Short.valueOf(String s)`: 将字符串参数解析为短整型，并返回一个 `Short` 实例。
- `Short.valueOf(short s)`: 返回一个表示指定短整数的 `Short` 实例。

#### Character

- `Character.isDigit(char ch)`: 判断指定字符是否为数字。
- `Character.isLetter(char ch)`: 判断指定字符是否为字母。
- `Character.isWhitespace(char ch)`: 判断指定字符是否为空白字符。
- `Character.toUpperCase(char ch)`: 将指定字符转换为大写字符。
- `Character.toLowerCase(char ch)`: 将指定字符转换为小写字符。
- `Character.valueOf(char c)`: 返回一个表示指定字符的 `Character` 实例。

### String

#### 声明

`String str = "Hello World!";`

`String str2 = new String("Hello World!");`

#### 常用函数

- `charAt(int index)`：返回指定索引处的字符。
- `length()`：返回字符串的长度。
- `equals(Object obj)`：判断两个字符串是否相等。
- `equalsIgnoreCase(String str)`：判断两个字符串是否相等，不区分大小写。
- `startsWith(String prefix)`：判断字符串是否以指定前缀开始。
- `endsWith(String suffix)`：判断字符串是否以指定后缀结束。
- `contains(String str)`：判断字符串是否包含指定子字符串。
- `replace(char oldChar, char newChar)`：替换字符串中的指定字符。
- `replaceAll(String regex, String replacement)`：替换字符串中的所有匹配正则表达式的子字符串。
- `split(String regex)`：分割字符串，返回字符串数组。
- `trim()`：去除字符串两端的空白字符。
- `substring(int beginIndex)`：返回从指定索引开始到结尾的子字符串。
- `substring(int beginIndex, int endIndex)`：返回从指定索引开始到指定索引结束的子字符串。
- `toLowerCase()`：将字符串转换为小写。
- `toUpperCase()`：将字符串转换为大写。
- `toCharArray()`：将字符串转换为字符数组（注意：此方法没有 `int srcBegin, int srcEnd` 参数，可能是您误记了）。

  **注意**：如果您想转换字符串的子序列为字符数组，可以先使用 `substring` 方法获取子字符串，然后再调用 `toCharArray()`。
- `toString()`：将字符串转换为字符串（此方法对于 `String` 对象本身来说是冗余的，因为调用它的对象已经是字符串类型）。

#### 串池

> String 常量池是 JVM 内部的一种缓存机制，它存储了已经创建过的 String 对象，当再次创建相同的 String 对象时，JVM 会直接从常量池中返回引用，而不是再次创建对象。因此，String 对象的创建和销毁非常快，所以在 Java 程序中尽量使用 String 常量池来避免创建过多的 String 对象。

```java
String str1 = "Hello";
String str2 = "Hello";
System.out.println(str1 == str2); // true
String str3 = new String("Hello");
System.out.println(str1 == str3); // false
```

对于相同内容的 String 对象，JVM 会缓存一个引用，因此 str1 和 str2 指向的是同一个对象，而 str3 指向的是一个新的对象。 因此，在 Java 程序中，尽量使用 String 常量池来避免创建过多的 String 对象，以提高程序的运行效率。

#### StringBuild

> StringBuilder 类是一个可变的字符序列，可以存储和操作文本信息。

```java
StringBuilder sb = new StringBuilder();
sb.append("Hello");
sb.append(" World!");
System.out.println(sb.toString()); // Hello World
StringBuilder sb2 = new StringBuilder("Hello World!");
System.out.println(sb2.toString());
```

#### StringJoiner

> StringJoiner 类是一个可变的字符序列，可以存储和操作文本信息。

```java
StringJoiner sj = new StringJoiner(", ", "[", "]");
sj.add("Hello");
sj.add("World!");
System.out.println(sj.toString()); // [Hello, World!]
StringJoiner sj2 = new StringJoiner(", ", "(", ")");
sj2.add("Hello");
sj2.add("World!");
System.out.println(sj2.toString()); // (Hello, World!)
```

### 集合

Java语言的集合是一种有序集合，可以存储多个相同类型的值。

Java语言提供了以下几种集合：

Collection

- List：列表，元素有序、可重复

  - Vector：顺序表（已废弃）
  - ArrayList：顺序表
  - LinkedList：链表

- Set：集合，元素无序、不可重复

  - HashSet：无序，不重复，无索引

    - LinkedHashSet：有序，不重复，无索引

  - TreeSet：可排序（从小到大），不重复，无索引

    > - 自定义类型需要实现 Comparable 接口，重写里面的抽象方法，指定比较规则
    >
    >   1. 默认排序/自然排序
    >
    >      ```java
    >      @Override
    >      public int compareTo(String o) {
    >          return this.getAge() - o.getAge();
    >      }
    >      ```
    >
    >      this：表示当前添加的元素
    >
    >      o：表示红黑树之前已经存在的元素
    >
    >      **返回值**
    >
    >      负值：认为要添加的元素是小的，存左边
    >
    >      正值：认为要添加的元素是大的，存右边
    >
    >      0：认为要添加的元素已经存在，舍弃
    >
    >   2. 比较器排序
    >
    >      ```java
    >      TreeSet<String> ts = new TreeSet<>((o1, o2) -> {
    >              // 按照长度排序
    >              int i = o1.length() - o2.length();
    >              // 如果长度一样按照默认首字母排序
    >              i = i == 0 ? o1.compareTo(o2) : i;
    >              return i;
    >      });
    >      ```
    >
    >      o1：表示当前添加的元素
    >
    >      o2：表示红黑树之前已经存在的元素
    >


List Set 的遍历方式

```java
// 迭代器遍历
Iterator<Student> it = stu.iterator();
while (it.hasNext()) {
    Student s = it.next();
    System.out.println(s);
}

// 增强 for 遍历
for (Student s : stu) {
    System.out.println(s);
}

// forEach() 遍历
stu.forEach(student -> System.out.println(student));
```

Map

- HashMap：无序，不重复，无索引
  - LinkedHashMap：有序，不重复，无索引
- Hashtable（HashMap 已替代，有线程安全性）
  - Properties


- TreeMap：可排序（从小到大），不重复，无索引

Entry

> Entry 是 Map 的子类，作用类似 CPP 的 pair 用来存储键值对



Map 的遍历方式

```java
// 传统 for-each
Set<Student> stuSet = stu.keySet();
for (Student s : stuSet) {
    if (s.getName().equals("小花")) {
        System.out.println(stu.get(s));
        break;
    }
}

// forEach() 遍历
stu.forEach(new BiConsumer<Student, Integer>() {
    @Override
    public void accept(Student student, Integer integer) {
        if (student.getName().equals("小花")) {
            System.out.println(integer);
        }
    }
});

// Entry 遍历

```

#### Collections

public static <T> boolean addAll(Collection<T> c, T... elements)：批量添加元素
public static void shuffle(List<?> list)：打乱List集合元素的顺序
public static <T> void sort(List<T> list)：排序
public static <T> void sort(List<T> list, Comparator<T> c)：根据指定的规则进行排序
public static <T> int binarySearch (List<T> list, T key)：以二分查找法查找元素
public static <T> void copy(List<T> dest, List<T> src)：拷贝集合中的元素
public static <T> int fill 1 (List<T> list,T obj)：使用指定的元素填充集合
public static <T> void max/min(Collection<T> coll)：根据默认的自然排序获取最大/小值
public static <T> void swap(list<?> list, int i, int j)：交换集合中指定位置的元素



#### List

> List 接口是一种有序的集合，元素可以重复。

- boolean add(E e)：添加元素到列表末尾
- void add(int index, E element)：添加元素到指定位置
- boolean addAll(Collection c)：添加集合中的所有元素到列表末尾
- boolean addAll(int index, Collection c)：添加集合中的所有元素到指定位置
- void clear()：清空列表
- boolean contains(Object o)：判断列表中是否包含指定元素
- boolean containsAll(Collection c)：判断列表中是否包含指定集合中的所有元素
- int indexOf(Object o)：返回指定元素在列表中的索引
- int lastIndexOf(Object o)：返回指定元素在列表中的最后一个索引
- ListIterator listIterator()：返回列表的迭代器
- ListIterator listIterator(int index)：返回指定位置的列表的迭代器
- E remove(int index)：删除指定位置的元素
- boolean remove(Object o)：删除指定元素
- boolean removeAll(Collection c)：删除指定集合中的所有元素
- boolean retainAll(Collection c)：保留指定集合中的元素
- E set(int index, E element)：设置指定位置的元素
- int size()：返回列表的大小
- List subList(int fromIndex, int toIndex)：返回指定范围的列表
- Object[] toArray()：返回列表中的所有元素组成的数组
- T[] toArray(T[] a)：返回列表中的所有元素组成的数组

```java
List list = new ArrayList<>();
list.add("Hello");
list.add("World!");
list.add(1, "Java");
list.addAll(Arrays.asList("Java", "Python"));
list.remove(1);
list.set(0, "Java");
System.out.println(list);
System.out.println(list.size());
System.out.println(list.get(0));
System.out.println(list.contains("Java"));
System.out.println(list.indexOf("Java"));
System.out.println(list.subList(1, 3));
```

#### Set

> Set 接口是一种无序的集合，元素不可重复。

- boolean add(E e)：添加元素到集合
- boolean addAll(Collection c)：添加集合中的所有元素到集合
- void clear()：清空集合
- boolean contains(Object o)：判断集合中是否包含指定元素
- boolean containsAll(Collection c)：判断集合中是否包含指定集合中的所有元素
- boolean isEmpty()：判断集合是否为空
- Iterator iterator()：返回集合的迭代器
- boolean remove(Object o)：删除指定元素
- boolean removeAll(Collection c)：删除指定集合中的所有元素
- boolean retainAll(Collection c)：保留指定集合中的元素
- int size()：返回集合的大小
- Object[] toArray()：返回集合中的所有元素组成的数组
- T[] toArray(T[] a)：返回集合中的所有元素组成的数组

```java
Set set = new HashSet<>();
set.add("Hello");
set.add("World!");
set.add("Java");
set.add("Java");
set.remove("Java");
System.out.println(set);
System.out.println(set.size());
System.out.println(set.contains("Java"));
System.out.println(set.toArray());
```

#### Map

> Map 接口是一种无序的集合，元素的键值对。

- void clear()：清空映射
- boolean containsKey(Object key)：判断映射中是否包含指定键
- boolean containsValue(Object value)：判断映射中是否包含指定值
- Set> entrySet()：返回映射中的所有键值对
- V get(Object key)：返回指定键对应的值
- boolean isEmpty()：判断映射是否为空
- Set keySet()：返回映射中的所有键
- V put(K key, V value)：添加或修改键值对
- void putAll(Map m)：添加或修改映射中的所有键值对
- V remove(Object key)：删除指定键对应的值
- int size()：返回映射的大小
- Collection values()：返回映射中的所有值

```java
Map map = new HashMap<>();
map.put("Hello", 1);
map.put("World!", 2);
map.put("Java", 3);
map.put("Java", 4);
map.remove("Java");
System.out.println(map);
System.out.println(map.size());
System.out.println(map.containsKey("Java"));
System.out.println(map.get("Java"));
System.out.println(map.entrySet());
```

#### 可变参数

```java
public static int getSum(int...args) {
    int sum = 0;
    for (int i : args)
        sum += i;
    return sum;
}
int sum = getSum(1, 2, 3, 4, 5);
```

1. 在方法的形参中最多只能写一个可变参数
2. 有多个形参，可变参数要放在最后

#### 不可变集合

> JDK9 新增，只能查询不可增删
>
> Map 的 of 之能传递 20 个参数，10 个键值对

static <E> List<E> of(E...elements)：创建一个具有指定元素的List集合对象
static <E> Set<E> of(E...elements)：创建一个具有指定元素的Set集合对象
static <K, V> Map<K, V> of(E...elements)：创建一个具有指定元素的Map集合对象

map.ofEntry(Map.Entry[]); // 返回不可修改的 Map

copyOf(); // 直接复制 // JDK 10 加入

```java
List<String> list = List.of()
    
Map.Entry[] arr1 = new Map.Entry[10];
Map map = Map.ofEntries(arr1);

```



### 二叉树

#### 二叉搜索树

二叉搜索树（Binary Search Tree，BST）是一种特殊的二叉树

- 左子树中的每个节点的值都小于它的根节点的值
- 右子树中的每个节点的值都大于它的根节点的值
- 左子树和右子树都是二叉搜索树

#### 二叉排序树

二叉排序树（Binary Sort Tree，BST）是一种特殊的二叉树

- 左子树中的每个节点的值都小于它的根节点的值
- 右子树中的每个节点的值都大于它的根节点的值
- 左子树和右子树都是二叉排序树
- 左子树的所有节点的值都比根节点的值小
- 右子树的所有节点的值都比根节点的值大

#### 平衡二叉树

平衡二叉树（Balanced Binary Tree，BBT）是一种特殊的二叉树

- 左右子树的高度差的绝对值不超过 1
- 左右子树都是平衡二叉树

#### 红黑树

红黑树（Red-Black Tree，RBT）是一种特殊的二叉搜索树

- 每个节点或者是红色的，或者是黑色的
- 根节点是黑色的
- 每个叶子节点（NIL）是黑色的
- 如果一个节点是红色的，则它的子节点必须是黑色的
- 对于每个节点，从该节点到其子孙节点的所有路径上包含相同数目的黑色节点

##### 红黑树添加节点规则

根

- 直接变成黑色

非根

- 父节点黑色
  - 不需要任何操作
- 父节点红色
  - 叔叔红色
    1. 将父节点和叔叔节点设为黑色
    2. 将祖父节点设为红色
    3. 如果祖父为根，将根变回黑色
    4. 如果祖父非根，将祖父设置为当前节点再进行其他判断
  - 叔叔黑色，当前节点为父节点的右孩子
    - 将父节点设为当前节点并左旋，再进行判断
  - 叔叔黑色，当前节点为父节点的左孩子
    1. 将父节点设为黑色
    2. 将祖父节点设为红色
    3. 以祖父为支点进行右旋

#### 左旋和右旋

左旋

。。。。。。

右旋

。。。。。。

## 类

### 方法

> Java语言的函数是由方法定义的

```java
public static void main(String[] args) {
    System.out.println("Hello World!");
}
```

### 类

Java语言的类是由类定义的，类的声明语法如下：

```java
public class Person {
    private String name;
    private int age;
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    public void sayHello() {
        System.out.println("Hello, my name is " + name + " and I am " + age + " years old.");
    }
}
```

#### 权限修饰符

- public：公共权限，可以在任何地方被访问
- private：私有权限，只能在当前类中被访问
- protected：受保护权限，可以在同一个包、子类中被访问
- default：默认权限，可以在同一个包中被访问

#### 多态

创建对象（多态方式）

```java
class Animal {
    String name = "动物";
    public void eat() {
        System.out.println("动物会吃东西！");
    }
}

class Dog extends Animal {
    String name = "狗";
    @Override
    public void eat() {
        System.out.println("狗会吃骨头！");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal animal = new Dog();
        System.out.println(animal.name); // 输出：动物
        animal.eat(); // 输出：狗会吃骨头！
    }
}
```

调用成员变量：编译看左边，运行看左边
animal 是 Animal 类型，name 是 Animal 类中的成员变量，所以编译看左边，运行看左边
调用成员方法：编译看左边，运行看右边

#### instanceof

```java
Person p = new Student();
if (p instanceof Student) { // 判断 p 是否是 Student 类型
    Student s = (Student)p;
    s.study();
}
// JDK14 及以上版本
if (p instanceof Student s) { // 声明变量 s 并赋值
    s.study();
}
```

#### 静态代码块

静态代码块在类被加载时执行，只执行一次，在静态代码块中可以定义类变量、静态方法、静态代码块。

```
public class MyClass { static { // 静态代码块 } }
```

#### 抽象类

抽象类是一种特殊的类，它不能实例化，只能作为基类被继承，抽象类可以包含抽象方法和具体方法，抽象方法不能有方法体，只能声明，具体方法可以有方法体。

```java
public abstract class Animal {
    public abstract void eat();
}
```

#### 内部类

1. 成员内部类：在类中定义的类，可以访问外部类的所有成员，包括私有成员。

成员内部类可以被修饰符修饰，包括 public、private、protected、default。
JDK16 及以上版本可以在成员内部类里面定义静态变量和静态方法。

```java
public class OuterClass {
    private int a = 10;
    public class InnerClass {
        private int a = 20;
        public void show() {
            int a = 30;
            System.out.println(a); // 输出：30
            System.out.println(this.a); // 输出：20
            System.out.println(OuterClass.this.a); // 输出：10
        }
    }
}

public class Main {
    public static void main(String[] args) {
        OuterClass outer = new OuterClass();
        OuterClass.InnerClass inner = outer.new InnerClass();
        // OuterClass.InnerClass inner = new OuterClass.new InnerClass(); 第二种方法
        inner.sayHello();
    }
}
```

2.静态内部类

```java
public class OuterClass {
    private String name = "外部类";
    public void sayHello() {
        System.out.println("Hello, my name is " + name + "!");
    }
    public static class InnerClass {
        public void sayHello() {
            System.out.println("Hello, my name is " + name + "!");
        }
    }
}

public class Main {
    public static void main(String[] args) {
        OuterClass.InnerClass inner = new OuterClass.InnerClass(); // 静态内部类不用再 new 实例化
        inner.sayHello();
    }
}
```

3.匿名内部类

匿名内部类是一种没有名字的内部类，可以简化代码。
可以写在成员位置，也可以写在局部位置。

```java
public class Main {
    public static void main(String[] args) {
        new Thread(new Runnable() {
            public void run() {
                System.out.println("Hello, world!");
            }
        }).start();
    }
}

new 接口或类名() {
    // 实现接口或类的方法
};
```

### final

Java语言的 final 关键字用于修饰类、方法、变量，用于防止修改。

- final 修饰类：表示该类不能被继承
- final 修饰方法：表示该方法不能被重写
- final 修饰变量：表示该变量只能被赋值一次

final 修饰引用类型：记录的地址值不能改变，内部属性值可以改变

### 接口

Java语言的接口是由接口定义的，接口的声明语法如下：

```java
public interface 接口名 {
    // 常量
    public static final 数据类型 常量名 = 数据值;
    // 抽象方法
    public abstract 返回值类型 方法名(参数类型 参数名, 参数类型 参数名, …);
    // 默认方法
    public default 返回值类型 方法名(参数类型 参数名, …) {
        // 方法体
    }
}     

// 实现接口
public class Dog implements Animal {}
```

例如：

```java
public interface Animal {
    public void eat();
}            
```

#### 标记型接口

接口内部没有抽象方法

### 泛型

Java语言的泛型是一种参数化类型，可以让代码更加灵活、类型安全。

```java
public class MyClass<T> {
    private T data;
    public MyClass(T data) {
        this.data = data;
    }
    public T getData() {
        return data;
    }
    public void setData(T data) {
        this.data = data;
    }
}          
```

#### 泛型通配符

泛型通配符 可以表示任何类型，例如 List 表示 List 集合中可以存放任意类型的元素。

泛型通配符 可以表示 T 及其子类类型，例如 List 表示 List 集合中可以存放 Animal 及其子类的元素。

泛型通配符 可以表示 T 及其父类类型，例如 List 表示 List 集合中可以存放 Animal 及其父类的元素。

## 常用API

### Math

还没写完...

### System

Java语言的 System 类提供了一系列静态方法，用于获取系统相关信息。

- public static void arraycopy(Object src, int srcPos, Object dest, int destPos, int length)：复制数组
- public static void exit(int status)：退出程序
- public static long currentTimeMillis()：返回当前时间（毫秒）

```java
public class Main {
    public static void main(String[] args) {
        int[] arr1 = {1, 2, 3};
        int[] arr2 = new int[3];
        System.arraycopy(arr1, 0, arr2, 0, 3);
        for (int i = 0; i < arr2.length; i++) {
            System.out.println(arr2[i]);
        }
    }
}
```



```java
System.out.println("Hello, world!");
```

其中 System 是类名，out 是 System 类的静态成员变量，println 是 System 类的静态方法。打印时将对象用 toString 方法转换为字符串。



### Runtime

Java语言的 Runtime 类提供了一系列方法，用于运行时环境。

- public static Runtime getRuntime()：获取运行时环境
- public static void exit(int status)：退出程序
- public int availableProcessors()：返回可用处理器数量
- public long maxMemory()：返回最大内存（单位：Byte）
- public long totalMemory()：返回总内存
- public long freeMemory()：返回剩余内存
- public Process exec(String command)：执行外部 CMD 命令

```java
public class Main {
    public static void main(String[] args) {
        Runtime runtime = Runtime.getRuntime();
        System.out.println("可用处理器数量：" + runtime.availableProcessors());
        System.out.println("最大内存：" + runtime.maxMemory() / 1024 / 1024 + "MB");
        System.out.println("总内存：" + runtime.totalMemory() / 1024 / 1024 + "MB");
        System.out.println("剩余内存：" + runtime.freeMemory() / 1024 / 1024 + "MB");
    }
}
```

### Object

Java语言的 Object 类提供了一系列方法，用于操作对象。

- public boolean equals(Object obj)：判断两个对象是否相等，默认比较地址值
- public int hashCode()：返回对象的哈希值
- public String toString()：返回对象的字符串表示，可以重写 toString 方法来改变默认的println输出
- clone()：创建对象的副本，默认调用 Object 类中的 clone 方法，默认为浅克隆(浅克隆：完全拷贝果赖；深克隆：基本数据类型拷贝过来，字符串复用，引用数据创建新的对象)

### BigInteger

Java语言的 BigInteger 类提供了对大整数的支持。

- public BigInteger(String val)：根据字符串创建 BigInteger 对象
- public BigInteger(int val)：根据 int 创建 BigInteger 对象
- public BigInteger(BigInteger val)：根据 BigInteger 对象创建 BigInteger 对象
- public BigInteger.valueof(long val)：根据 long 创建静态 BigInteger 对象，会提前创建好-16到16的缓存
- public BigInteger add(BigInteger val)：加法，对象一旦创建就不可改变
- public BigInteger subtract(BigInteger val)：减法
- public BigInteger multiply(BigInteger val)：乘法
- public BigInteger divide(BigInteger val)：除法
- public BigInteger remainder(BigInteger val)：取模
- public BigInteger pow(int exponent)：求幂
- public int compareTo(BigInteger val)：比较大小
- public BigInteger abs()：取绝对值
- public BigInteger negate()：取相反数
- public BigInteger max/min(BigInteger val)：取最大/最小值
- public int intValue()：返回 BigInteger 值对应的 int 值

### BigDecimal

Java语言的 BigDecimal 类提供了对 BigDecimal 的支持。

- public BigDecimal(String val)：根据字符串创建 BigDecimal 对象
- public BigDecimal(double val)：根据 double 创建 BigDecimal 对象
- public BigDecimal(BigDecimal val)：根据 BigDecimal 对象创建 BigDecimal 对象
- public BigDecimal.valueOf(long val)：根据 long 创建静态 BigDecimal 对象，会提前创建好0到10的缓存
- public BigDecimal add(BigDecimal val)：加法，对象一旦创建就不可改变
- public BigDecimal subtract(BigDecimal val)：减法
- public BigDecimal multiply(BigDecimal val)：乘法
- public BigDecimal divide(BigDecimal val)：除法
- public BigDecimal remainder(BigDecimal val)：取模
- public BigDecimal pow(int exponent)：求幂
- public int compareTo(BigDecimal val)：比较大小
- public BigDecimal abs()：取绝对值
- public BigDecimal negate()：取相反数
- public BigDecimal max/min(BigDecimal val)：取最大/最小值
- public double doubleValue()：返回 BigDecimal 值对应的 double 值

### Random

Java语言的 Random 类提供了随机数生成器。

- public Random()：构造方法，使用默认种子
- public Random(long seed)：构造方法，使用指定种子
- public void setSeed(long seed)：设置种子
- public int nextInt()：返回一个随机 int 值
- public int nextInt(int bound)：返回一个随机 int 值，范围为 [0, bound)
- public long nextLong()：返回一个随机 long 值
- public boolean nextBoolean()：返回一个随机 boolean 值
- public float nextFloat()：返回一个随机 float 值
- public double nextDouble()：返回一个随机 double 值
- public double nextGaussian()：返回一个符合高斯分布的随机 double 值

案例：

带有概率的随机点名

```java
ArrayList<Integer> list = new ArrayList<>();
Collections.addAll(list, 1, 1, 1, 1, 1, 1, 1);
Collections.addAll(list, 0, 0, 0);
Collections.shuffle(list);

Random r = new Random();
int index = r.nextInt(list.size());
int number = list.get(index);

ArrayList<String> boyList = new ArrayList<>();
ArrayList<String> girlList = new ArrayList<>();
Collections.addAll(boyList, "小王", "小张", "小李", "李华", "张三", "李四", "王五", "小马");
Collections.addAll(girlList, "小花", "小美", "小丽");

if (number == 1) {
    int boyIndex = r.nextInt(boyList.size());
    System.out.println(boyList.get(boyIndex));
} else {
    int girlIndex = r.nextInt(girlList.size());
    System.out.println(girlList.get(girlIndex));
}
```



### 正则表达式

Java语言的正则表达式支持。

正则表达式语法（只匹配一个字符）

- [abc]：匹配 a、b、c 中的任意一个字符
- [^abc]：匹配除了 a、b、c 以外的任意一个字符
- [a-z]：匹配 a 到 z 范围内的任意一个字符
- [a-zA-Z]：匹配 a 到 z A 到 Z 范围内的任意一个字母
- [a-z&&[def]]：匹配 a 到 z 范围内的 d、e、f 中的任意一个字符
- [^a-z]：匹配除了 a 到 z 范围以外的任意一个字符
- .：匹配任意一个字符
- \d：匹配任意一个数字
- \D：匹配任意一个非数字
- \s：匹配任意一个空白字符
- \S：匹配任意一个非空白字符
- \w：匹配任意一个字母、数字或下划线
- \W：匹配任意一个非字母、数字或下划线

> ###### \是转义字符，\\就是\，\\d就是\d，所以要表达\d就要写成\\d

正则表达式语法（匹配多个字符）

- a*：匹配 0 个或多个 a
- a+：匹配 1 个或多个 a
- a?：匹配 0 个或 1 个 a
- a{n}：匹配 n 个 a
- a{n,}：匹配 n 个或多个 a
- a{n,m}：匹配 n 到 m 个 a
- a|b：匹配 a 或 b

正则表达式类

- Pattern 类：用于创建正则表达式对象
- public static Pattern compile(String regex)：编译正则表达式
- Matcher 类：用于匹配正则表达式
- public static Matcher matcher(String regex, String input)：创建 Matcher 对象
- public static boolean matches(String regex, String input)：判断字符串是否匹配正则表达式
- public boolean Matcher.find()：寻找是否有匹配的字符串
- public String Matcher.group()：返回匹配的字符串
- public String[] Matcher.group(int group)：返回第 group 组匹配的字符串
- public static String replaceAll(String regex, String input, String replacement)：替换字符串中所有匹配正则表达式的部分
- public static String[] split(String regex, String input)：分割字符串

### 时间

### 时间格式

| 子母 | 日期或时间元素          | 表示              | 示例                                  |
| ---- | ----------------------- | ----------------- | ------------------------------------- |
| G    | Era 标志符              | Text              | AD                                    |
| y    | 年                      | Year              | 1996; 96                              |
| M    | 年中的月份              | Month             | July: Jul; 07                         |
| w    | 年中的周数              | Number            | 27                                    |
| W    | 月份中的周数            | Number            | 2                                     |
| D    | 年中的天数              | Number            | 189                                   |
| d    | 月份中的天数            | Number            | 10                                    |
| F    | 月份中的星期            | Number            | 2                                     |
| E    | 星期中的天数            | Text              | Tuesday; Tue                          |
| a    | Am/pm 标记              | Text              | PM                                    |
| H    | 一天中的小时数 (0-23)   | Number            | 0                                     |
| k    | 一天中的小时数 (1-24)   | Number            | 24                                    |
| K    | am/pm中的小时数（0-11)  | Number            | 0                                     |
| h    | am/pm 中的小时数（1-12) | Number            | 12                                    |
| m    | 小时中的分钟数          | Number            | 30                                    |
| s    | 分钟中的秒数            | Number            | 55                                    |
| S    | 毫秒数                  | Number            | 978                                   |
| z    | 时区                    | General time zone | Pacific Standard Time; PST; GMT-08:00 |
| Z    | 时区                    | REC-822 time zone | -0800                                 |

2023-11-11 13:27:06
yyyy-MM-dd HH:mm:SS

#### JDK7及以前

Data类

| 方法名称                       | 说明                       |
| ------------------------------ | -------------------------- |
| public Date()                  | 创建Date对象，表示当前时间 |
| public Date(long date)         | 创建Date对象，表示指定时间 |
| public void setTime(long time) | 设置/修改毫秒值            |
| public long getTime()          | 获取时间对象的毫秒值       |

```java
//1.创建对象表示一个时间
Date d1 = new Date();
System.out.println(d1); // Thu Jan 01 08:00:00 CST 1970
//2.创建对象表示一个指定的时间
Date d2 = new Date(0L);
System.out.println(d2);
//3.setTime修改时间
//1000毫秒=1秒
d2.setTime(1000L);
System.out.println(d2);
//4.getTime获取当前时间的毫秒值
long time = d2.getTime();
System.out.println(time);
```

SimpleDateFormat类

| 构造方法                                | 说明                                                     |
| --------------------------------------- | -------------------------------------------------------- |
| public SimpleDateFormat()               | 构造一个simpleDateFormat，使用默认格式 1970/1/1 上午8:00 |
| public SimpleDateFormat(String pattern) | 构造一个simpleDateFormat，使用指定的格式                 |

| 常用方法                              | 说明                        |
| ------------------------------------- | --------------------------- |
| public final String format(Date date) | 格式化（日期对象 -> 字符串) |
| public Date parse(String source)      | 解析 (字符串 -> 日期对象)   |

```java
//1.定义一个字符串表示时间
String str ="2023-11-11 11:11:11"
//2.利用空参构造创建SimpleDateFormat对象
//细节：
//创建对象的格式要跟字符串的格式完全一致
SimpleDateFormat sdf = new SimpleDateFormat( pattern: "yyyy-MM-dd HH:mm:ss");
Date date = sdf.parse(str);
//3.打印结果
System.out.println(date)
// Sat Nov 11 11:11:11CST 2023
```

Calendar类

`public static Calendar getInstance()` 获取当前时间的日历对象

| 方法名                                   | 说明                        |
| ---------------------------------------- | --------------------------- |
| public final Date getTime()              | 获取日期对象                |
| public final setTime(Date date)          | 给日历设置日期对象          |
| public long getTimeInMillis()            | 拿到时间毫秒值              |
| public void setTimeInMillis(long millis) | 给日历设置时间毫秒值        |
| public int get(int field)                | 取日历中的某个字段信息      |
| public void set(int field, int value)    | 修改日历的某个字段信息      |
| public void add(int field, int amount)   | 为某个字段增加/减少指定的值 |

细节

Calendar是一个抽象类，不能直接new，而是通过一个静态方法获取到子类对象
底层原理：
会根据系统的不同时区来获取不同的日历对象，默认表示当前时间。
把会把时间中的纪元，年，月，日，时，分，秒，星期，等等的都放到一个数组当中
0：纪元<br/>1：年<br/>2：月<br/>3：一年中的第几周<br/>4：一个月中的第几周<br/>5：一个月中的第几天（日期）<br/>...<br/>16

月份：范围0~11如果获取出来的是0.那么实际上是1月。
星期：在老外的眼里，星期日是一周中的第一天
1(星期日）2（星期一）3（星期二）4（星期三）5（星期四）6（星期五）7(星期六)

#### JDK8新增

懒得学了

## <a id = "Stream流">[Stream流](#JAVA)</a>

### Stream流的获取

| 获取方式     | 方法名                                        | 说明                     |
| ------------ | --------------------------------------------- | ------------------------ |
| 单列集合     | defaultStream<E>stream()                      | Collection中的默认方法   |
| 双列集合     | 无                                            | 无法直接使用stream流     |
| 数组         | public static <T> Stream<T> stream(T[] array) | Arrays工具类中的静态方法 |
| 一堆零散数据 | public static<T> Stream<T> of(T... values)    | Stream接口中的静态方法   |

Stream 接口中静态方法 of 的细节
方法的形参是一个可变参数，可以传递一堆零散的数据，也可以传递数组
但是数组必须是引用数据类型的，如果传递基本数据类型，是会把整个数组当做一个元素，放到 stream 当中。

### Stream流的中间方法

| 名称                                             | 说明                                 |
| ------------------------------------------------ | ------------------------------------ |
| Stream<T> filter(Predicate<? super T> predicate) | 过滤                                 |
| Stream<T> limit(long maxSize)                    | 获取前几个元素                       |
| Stream<T> skip(long n)                           | 跳过前几个元素                       |
| Stream<T> distinct()                             | 元素去重，依赖(hashCode和equals方法) |
| static<T> Stream<T> concat(Stream a, Stream b)   | 合并a和b两个流为一个流               |
| Stream<R> map(Function<T , R> mapper)            | 转换流中的数据类型                   |

注意1：中间方法，返回新的Stream流，原来的Stream流只能使用一次，建议使用链式编程
注意2：修改Stream流中的数据，不会影响原来集合或者数组中的数据

### Stream流的终结方法

| 名称                          | 说明                       |
| :---------------------------- | :------------------------- |
| void forEach(Consumer action) | 遍历                       |
| long count()                  | 统计                       |
| toArray()                     | 收集流中的数据，放到数组中 |
| collect(Collector collector)  | 收巢流中的数据，放到集合中 |

collect详解



## 方法引用

1.引用静态方法
类名::静态方法

2．引用成员方法
对象::成员方法
this::成员方法
super::成员方法

3．引用构造方法
类名::new

4.使用类名引用成员方法
类名::成员方法

5.引用数组的构造方法
数据类型[]::new

## 异常

> 异常的作用
> 作用一：异常是用来查询bug的关键参考信息
> 作用二：异常可以作为方法内部的一种特殊返回值，以便通知调用者底层的执行情况

Java.lang.Throwable

- Error
- Exception
  - RuntimeException
    - ......
  - 其他异常

### 异常的处理方式

#### JVM默认的处理方式

把异常的名称，异常原因及异常出现的位置等信息输出在了控制台
程序停止执行下面的代码不会再执行了

#### 自己处理（捕获异常）

```java
try {
    // 可能异常的代码
} catch(异常类名 变量名) {
    // 异常的处理代码
} finally {
    // 最后一定执行，除非虚拟机停止
}
```

目的：当代码出现异常时，可以让程序继续往下执行。

#### 抛出异常

##### throws

写在方法定义处，表示声明一个异常，告诉调用者，使用本方法可能会有哪些异常

```java
public void 方法()throws 异常类名1, 异常类名2, ... {
    // code
}
```

编译时异常：必须要写。
运行时异常：可以不写。

##### throw

写在方法内，结束方法
手动抛出异常对象交给调用者
方法中下面的代码不再执行了

```java
public void 方法() {
	throw new NullPointerException();
}
```

### 自定义异常类

类名末尾加 `Exception` 表示当前类是一个异常类

#### 异常类的继承

运行时：RuntimeException 核心 就表示由于参数错误而导致的问题
编译时：Exception 核心 提醒程序员检查本地信息

### 异常中的常见方法

#### Throwable的成员方法

| 方法名称                     | 说明                                     |
| ---------------------------- | ---------------------------------------- |
| public String getMessage()   | 返回此 throwable 的详细消息字符串        |
| public String tostring()     | 返回此可抛出的简短描述                   |
| public voidprintstackTrace() | 把异常的错误信息输出在控制台(System.err) |

### 一些细节

try中遇到多个问题可以写多个catch与之对应，如果我们要捕获多个异常，这些异常中存在父子关系的话，那么父类一定要写在下面

在JDk7之后，我们可以在catch中同时捕获多个异常，中间用|进行隔开
表示如果出现了A异常或者B异常的话，采取同一种处理方案

如果try中遇到了问题，那么try下面的其他代码还会执行吗？
下面的代码就不会执行了，直接跳转到对应的catch当中，执行catch里面的语句体
但是如果没有对应catch与之匹配，那么还是会交给虚拟机进行处理

#### 运行时异常和编译时异常的区别

编译时异常：除了RuntimeExcpetion和他的子类，其他都是编译时异常
编译阶段需要进行处理，作用在于提醒程序员。

运行时异常：RuntimeException本身和所有子类，都是运行时异常。
编译阶段不报错，是程序运行时出现的。
一般是由于参数传递错误带来的问题

## 文件

### File构造方法

| 方法名称                                 | 说明                                               |
| ---------------------------------------- | -------------------------------------------------- |
| public File(String pathname)             | 根据文件路径创建文件对象                           |
| public File(String parent, String child) | 根据父路径名字符串和子路径名字符串创建文件对象     |
| public File(File parent, String child)   | 根据父路径对应文件对象和子路径名字符串创建文件对象 |

```java
//1.根据字符串表示的路径，变成File对象
String str ="C:\\Users\lalienware\\Desktop\la.txt";
File f1 = new File(str);
System.out.println(f1);//C:\Users\alienware\Desktop\a.txt
//2.父级路径：C:\Users\alienware\Desktop
//子级路径：a.txtE

String parent = "C:\\Users\lalienware\\Desktop";
String child = "a.txt";
File f2 = new File(parent,child);
System.out.println(f2);//C:\Users\alienware\Desktop\a.txt
File f3 = new File( pathname: parent + "\\" + child);
System.out.println(f3);//C:\Users\alienware\Desktop\a.txt

//3.把一个File表示的路径和String表示路径进行拼接
File parent2 = new File( pathname: "C:\\Users\\alienware\\Desktop");
String child2 = "a.txt";
File f4 = new File(parent2,child2);
System.out.println(f4);//C:\Users\alienware\Desktop\a.txt
```

### File常见的成员方法

#### 判断，获取

| 方法名称                        | 说明                                                    |
| ------------------------------- | ------------------------------------------------------- |
| public boolean isDirectory()    | 判断此路径名表示的File是否为文件夹                      |
| public boolean isFile()         | 判断此路径名表示的File是否为文件                        |
| public boolean exists()         | 判断此路径名表示的File是否存在                          |
| public long length()            | 返回文件的字节大小, 无法获取文件夹大小 (len / 1024): KB |
| public String getAbsolutePath() | 返回文件的绝对路径                                      |
| public String getPath()         | 返回定义文件时使用的路径(String)                        |
| public String getName()         | 返回文件的名称，带后缀                                  |
| public long lastModified()      | 返回文件的最后修改时间 (时间毫秒值)                     |

#### 创建，删除

| 方法名称                       | 说明                 |
| ------------------------------ | -------------------- |
| public boolean createNewFile() | 创建一个新的空的文件 |
| public boolean mkdir()         | 创建单级文件夹       |
| public boolean mkdirs()        | 创建多级文件夹       |
| public boolean delete()        | 删除文件、空文件夹   |

1.createNewFile
细节1：如果当前路径表示的文件是不存在的，则创建成功，方法返回true
如果当前路径表示的文件是存在的，则创建失败，方法返回false
细节2：如果父级路径是不存在的，那么方法会有异常IOException
细节3：createNewFile方法创建的一定是文件，如果路径中不包含后缀名，则创建一个没有后缀的文件

```java
File f1 = new File("D:\\aaa\\ddd");
boolean b = f1.createNewFile();
System.out.println(b);//true
```

2.mkdirmakeDirectory
细节1：windows当中路径是唯一的，如果当前路径已经存在，则创建失败，返回false
细节2：mkdir方法只能创建单级文件夹，无法创建多级文件夹。

```java
File f2= new File("D://aaa\/aaa\\bbb\/ccc");
booleanb = f2.mkdir（);
System.out.println(b);
```

3.public boolean delete()
如果删除的是文件，则直接删除，不走回收站。
如果删除的是空文件夹，则直接删除，不走回收站
如果删除的是有内容的文件夹，则删除失败

#### 获取，遍历

`public File[] listFiles()` 获取当前该路径下所有内容

```java
//1.创建File对象
File f = new File("D:\\aaa");
//2.listFiles方法
//作用：获取aaa文件夹里面的所有内容，把所有的内容放到数组中返回
File[] files = f.listFiles();
for (File file : files) {
//file依次表示aaa文件夹里面的每一个文件或者文件夹
	System.out.println(file);
}
```

当调用者File表示的路径不存在时，返回null
当调用者File表示的路径是文件时，返回null
当调用者File表示的路径是一个空文件夹时，返回一个长度为O的数组
当调用者File表示的路径是一个有内容的文件夹时，将里面所有文件和文件夹的路径放在File数组中返回
当调用者File表示的路径是一个有隐藏文件的文件夹时，将里面所有文件和文件夹的路径放在File数组中返回，包含隐藏文件
当调用者File表示的路径是需要权限才能访问的文件夹时，返回null

| 方法名称                                       | 说明                                     |
| ---------------------------------------------- | ---------------------------------------- |
| public static File[] listRoots()               | 列出可用的文件系统根                     |
| public String[] list()                         | 获取当前该路径下所有内容                 |
| public String[] list(FilenameFilter filter)    | 利用文件名过滤器获取当前该路径下所有内容 |
| public File[] listFiles()                      | 获取当前该路径下所有内容                 |
| public File[] listFiles(FileFilter filter)     | 利用文件名过滤器获取当前该路径下所有内容 |
| public File[] listFiles(FilenameFilter filter) | 利用文件名过滤器获取当前该路径下所有内容 |

剩下的懒得看了

## IO流

### 字节流

> 常用于处理二进制文件，视频、音频、图片等

#### InputStream

##### FileInputStream

字节输入流的细节：
1.创建字节输入流对象
细节1：如果文件不存在，就直接报错。
Java为什么会这么设计呢？
输出流：不存在，创建
把数据写到文件当中
输入流：不存在，而是报错呢？
因为创建出来的文件是没有数据的，没有任何意义。
所以Java就没有设计这种无意义的逻辑，文件不存在直接报错。
程序中最重要的是：数据。
2.写数据
细节1：一次读一个字节，读出来的是数据在ASCII上对应的数字
细节2：读到文件末尾了，read方法返回-1。
3.释放资源
细节：每次使用完流之后都要释放资源

| 方法名称                       | 说明                   |
| ------------------------------ | ---------------------- |
| public int read()              | 一次读一个字节数据     |
| public int read(byte[] buffer) | 一次读一个字节数组数据 |

复制文件完整代码

```java
//1.创建对象
FileInputStream fis = null;
FileOutputStream fos = null;
try {
    fis = new FileInputStream("D:\\itheima\\movie.mp4");
    fos = new FileOutputStream("myio\\copy.mp4");
    //2.拷贝
    int len;
    byte[] bytes = new byte[1024 * 1024 * 5];
    while ((len = fis.read(bytes)) != -1) {
        fos.write(bytes, 0, len);
    }
} catch (IOException e) {
    //e.printStackTrace();
} finally {
    //3.释放资源
    if (fos != null) {
        try {
            fos.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
    if (fis != null) {
        try {
            fis.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

JDK7：I0流中捕获异常的写法

```java
try后面的小括号中写创建对象的代码，
注意：只有实现了AutoCloseable接口的类，才能在小括号中创建对象。
try (创建流对象1;创建流对象2) {
    // code
} catch() {
    // 异常处理
}
```

JDK9方案

```java
创建流对象1;
创建流对象2;
try (流1;流2) {
    // code
} catch() {
    // 异常处理
}
```

#### OutputStream

##### FileOutputStream

操作本地文件的字节输出流，可以把程序中的数据写到本地文件中。

1.创建字节输出流对象
细节1：参数是字符串表示的路径或者是File对象都是可以的
细节2：如果文件不存在会创建一个新的文件，但是要保证父级路径是存在的。
细节3：如果文件已经存在，则会清空文件
2.写数据
细节：write方法的参数是整数，但是实际上写到本地文件中的是整数在ASCII上对应的字符
3.释放资源
每次使用完流之后都要释放资源

write函数

```java
void write(int b)
void write(byte[] b) // 一次写一个字节数组数据
void write(byte[] b, int off, int len) // 一次写一个字节数组的部分数据	参数一：数组	参数二：起始索引	参数三：个数
```

换行写：`\r\n`

续写：`FileOutputStream fos = new FileOutputStream("myio\\a.txt", true);`

### 字符流

> 常用于处理文本文件

Java中编码的方法

| String类中的方法                           | 说明                 |
| ------------------------------------------ | -------------------- |
| public byte[] getBytes()                   | 使用默认方式进行编码 |
| public byte[] getBytes(String charsetName) | 使用指定方式进行编码 |

Java中解码的方法

| String类中的方法                         | 说明                 |
| ---------------------------------------- | -------------------- |
| String(byte[] bytes)                     | 使用默认方式进行解码 |
| String(byte[] bytes, String charsetName) | 使用指定方式进行解码 |

```java
//1.编码
String str="ai你哟";
byte[] bytes1 = str.getBytes();
System.out.println(Arrays.toString(bytes1));
byte[] bytes2 = str.getBytes("GBK");
System.out.println(Arrays.toString(bytes2));
//2.解码
String str2 = new String(bytes1);
System.out.println(str2);
String str3 = new String(bytes1, "GBK");
System.out.println(str3);| I
```



#### Reader

FileReader

| 构造方法                           | 说明                       |
| ---------------------------------- | -------------------------- |
| public FileReader(File file)       | 创建字符输入流关联本地文件 |
| public FileReader(String pathname) | 创建字符输入流关联本地文件 |

| 成员方法                       | 说明                         |
| ------------------------------ | ---------------------------- |
| public int read()              | 读取数据，读到末尾返回-1     |
| public int read(char[] buffer) | 读取多个数据，读到末尾返回-1 |

细节1:按字节进行读取，遇到中文，一次读多个字节，读取后解码，返回一个整数
细节2:读到文件末尾了，read方法返回-1。

```java
//1.创建对象并关联本地文件
FileReader fr= new FileReader("myio\\a.txt");
//2.读取数据read()
//字符流的底层也是字节流，默认也是一个字节一个字节的读取的。
//如果遇到中文就会一次读取多个，GBK一次读两个字节，UTF-8一次读三个字节
//read（）细节：
//1.read（)：默认也是一个字节一个字节的读取的，如果遇到中文就会一次读取多个
//2.在读取之后，方法的底层还会进行解码并转成十进制。
//	最终把这个十进制作为返回值
//	这个十进制的数据也表示在字符集上的数字
//	英文：文件里面二进制数据01100001
//		read方法进行读取，解码并转成十进制97
//	中文：文件里面的二进制数据111001101011000110001001
//		read方法进行读取，解码并转成十进制27721
//我想看到中文汉字，就是把这些十进制数据，再进行强转就可以了
int ch;
while((ch = fr.read()) != -1){
System.out.print((char)ch);
//3.释放资源
fr.close();
```



#### Writer

FileWriter

| 构造方法                                           | 说明                             |
| -------------------------------------------------- | -------------------------------- |
| public FileWriter(File file)                       | 创建字符输出流关联本地文件       |
| public FileWriter(String pathname)                 | 创建字符输出流关联本地文件       |
| public FileWriter(File file, boolean append)       | 创建字符输出流关联本地文件，续写 |
| public FileWriter(String pathname, boolean append) | 创建字符输出流关联本地文件，续写 |

文件夹复制

```java
private static void copyDir(File parent, File parent2) throws IOException {
    parent2.mkdirs();
    File[] files = parent.listFiles();
    for (File file : files) {
        if (file.isFile()) {
            FileInputStream fis = new FileInputStream(file);
            FileOutputStream fos = new FileOutputStream(new File(parent2, file.getName()));
            byte[] bytes = new byte[1024 * 1024];
            int len;
            while ((len = fis.read(bytes)) != -1) {
                fos.write(bytes, 0, len);
            }
            fos.close();
            fis.close();
        } else {
            copyDir(file, new File(parent2, file.getName()));
        }
    }
}
```



### 缓冲流

> 底层自带了长度为8192的缓冲区提高性能

#### BufferedlnputStream

宇节缓冲输入流

#### BufferedOutputStream

宇节缓冲输出流

| 方法名称                                     | 说明                                     |
| -------------------------------------------- | ---------------------------------------- |
| public BufferedInputStream(InputStream is)   | 把基本流包装成高级流，提高读取数据的性能 |
| public BufferedOutputStream(OutputStream os) | 把基本流包装成高级流，提高写出数据的性能 |

```java
//1.创建缓冲流的对象
BufferedInputStream bis = new BufferedInputStream(new FileInputStream("myio\\a.txt"));
BufferedOutputStream bos =new BufferedOutputStream(new FileOutputStream("myio\\copy.txt"));
//2.循环读取并写到目的地
int b;
while （(b=bis.read()）!=-1){
	bos.write(b);
}
//3.释放资源
bos.close();
bis.close();
```

#### BufferedReader

字符缓冲输入流

#### BufferedWriter

字符缓冲输出流

| 方法名称                        | 说明               |
| ------------------------------- | ------------------ |
| public BufferedReader(Reader r) | 把基本流变成高级流 |
| public BufferedWriter(Writer r) | 把基本流变成高级流 |

字符缓冲流特有方法

字符缓冲输入流特有方法

`public String readLine()` 读取一行数据，如果没有数据可读了，会返回null

字符缓冲输出流特有方法

`public void newLine()` 跨平台的换行

```java
//1.创建字符缓冲输入流的对象
BufferedReader br=new BufferedReader(new FileReader("myio\la.txt"));
//2.读取数据
//细节：
//readLine方法在读取的时候，一次读一整行，遇到回车换行结束
//但是他不会把回车换行读到内存当中
String line;
while (((line = br.readLine()）!= null)) {
	System.out.println(line);
}
//3.释放资源
br.close();
       
//1.创建字符缓冲输出流的对象
BufferedWriter bw = new Bufferedwriter(new FileWriter("b.txt", true));
//2.写出数据
bw.write(str: "123");
bw.newLine();
bw.write(str: "456");
bw.newLine();
//3.释放资源R
bw.close();
```

### 转换流

> 字节流转换成字符流，也可以转换编码（JDK11被淘汰）
>
> 字节流使用字符流的功能

输入流

```java
//1.创建对象并指定字符编码
InputStreamReader isr = new InputStreamReader(new FileInputStream("myio\\gbkfile.txt"), "GBK");
//2.读取数据
int ch;
while ((ch = isr.read()) != -1){
System.out.print((char)ch);
//3.释放资源
isr.close();
```

替代方案

```java
FileReader fr = new FileReader("myio\\gbkfile.txt", Charset.forName("GBK"));
//2.读取数据
int ch;
while ((ch = fr.read()) != -1){
System.out.print((char)ch);
//3.释放资源
fr.close();
```

输出流

```java
//1.创建转换流的对象
OutputStreamWriter osw = new OutputStreamWriter(new FileOutputStream("myio\\b.txt"), "GBK");
//2.写出数据
osw.write("你好你好");
//3.释放资源
osw.close();
```

替代方案

```java
FileWriter fw = new FileWriter("myio\\c.txt", Charset.forName("GBK"));
fw.write("你好你好")；
fw.close();
```

### 序列化流

> 可以把 java 中的对象写到本地文件

`public ObjectOutputStream(OutputStream out)` 把基本流包装成高级流

`public final void writeObject(Object obj)` 把对象序列化（写出）到文件中去

```java
//1.创建对象
Student stu = new Student("zhangsan", 23);
//2.创建序列化流的对象/对象操作输出流
ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("myiolla.txt"));
//3.写出数据
oos.writeObject(stu);
//4.释放资源
oos.close();
```

使用对象输出流将对象保存到文件时会出现`NotSerializableException`异常

解决方案：需要让`Javabean`类实现`serializable`接口

#### 反序列化流

`public ObjectInputStream(InputStream out)` 把基本流变成高级流

`public Object readObject()` 把序列化到本地文件中的对象，读取到程序中来

```java
//1.创建反序列化流的对象
ObjectInputStream ois = new ObjectInputStream(new FileInputStream("myio\\la.txt"));
//2.读取数据
Object o = ois.readObject();
//3.打印对象
System.out.println(o);
//4.释放资源
ois.close();
```

细节：

1.序列化后修改Javabean然后再反序列化会报错，因为序列化后Javabean会有个版本号`serialVersionUID`对应不上，鼠标放在Javabean名字上加上即可

2.`transient` 瞬态关键字
作用：不会把当前属性序列化到本地文件当中

3.多个对象可以放在集合中进行序列化，然后再反序列化到集合中进行读取

### 打印流

特点1：打印流只操作文件目的地，不操作数据源
特点2:特有的写出方法可以实现，数据原样写出
	例如：打印：97	文件中：97	打印：true	文件中：true
特点3：特有的写出方法可以实现自动刷新，自动换行
      打印一次数据 = 写出 + 换行 + 刷新

#### 字节打印流

| 构造方法                                                     | 说明                         |
| ------------------------------------------------------------ | ---------------------------- |
| public PrintStream(OutputStream/File/String)                 | 关联字节输出流/文件/文件路径 |
| public PrintStream(String fileName, Charset charset)         | 指定字符编码                 |
| public PrintStream(OutputStream out, boolean autoFush)       | 自动刷新                     |
| public PrintStream(OutputStream out, boolean autoFlush, String encoding) | 指定字符编码且自动刷新       |

字节流底层没有缓冲区，开不开自动刷新都一样

| 成员方法                                          | 说明                                       |
| ------------------------------------------------- | ------------------------------------------ |
| public void write(int b)                          | 常规方法：规则跟之前一样，将指定的字节写出 |
| public void println(Xxx xx)                       | 特有方法：打印任意数据，自动刷新，自动换行 |
| public void print(Xxx xx)                         | 特有方法：打印任意数据，不换行             |
| public void printf(String format, Object... args) | 特有方法：带有占位符的打印语句，不换行     |



#### 字符打印流

| 构造方法                                                     | 说明                         |
| ------------------------------------------------------------ | ---------------------------- |
| public PrintWriter(Write/File/String)                        | 关联字节输出流/文件/文件路径 |
| public PrintWriter(String fileName, Charset charset)         | 指定字符编码                 |
| public PrintWriter(Write w, boolean autoFlush)               | 自动刷新                     |
| public PrintWriter(OutputStream out, boolean autoFlush, Charset charset) | 指定字符编码且自动刷新       |

字符流底层有缓冲区，想要自动刷新需要开启

成员方法和字节打印流的基本一样

### 解压缩流

```java
//定义一个方法用来解压
public static void unzip(File src,File dest) throws IOException {
    //解压的本质：把压缩包里面的每一个文件或者文件夹读取出来，按照层级拷贝到目的地当中
    //创建一个解压缩流用来读取压缩包中的数据
    ZipInputStream zip = new ZipInputStream(new FileInputStream(src));
    //要先获取到压缩包里面的每一个zipentry对象
    //表示当前在压缩包中获取到的文件或者文件夹
    ZipEntry entry;
    while((entry = zip.getNextEntry()) != null){
    	System.out.println(entry);
    	if(entry.isDirectory()){
            //文件夹：需要在目的地dest处创建一个同样的文件夹
            File file = new File(dest,entry.toString());
            file.mkdirs();
        else{
            //文件：需要读取到压缩包中的文件，并把他存放到目的地dest文件夹中（按照层级目录进行存放)
            FileoutputStream fos = new FileoutputStream(new File(dest,entry.toString()));
            int b;
            while((b = zip.read()) != -1){
                //写到目的地
                fos.write(b);
            }
            fos.close();
            //表示在压缩包中的一个文件处理完毕了。
            zip.closeEntry();
        }
    }
    zip.close();
}
```

### 解压缩流

```java
public static void toZip(File src,ZipoutputStream zos,String name） throws IOException {
    //1.进入src文件夹
    File[] files = src.listFiles();
    //2.遍历数组
    for (File file :files){
        if(file.isFile()){
            //3.判断-文件，变成zipEntry对象，放入到压缩包当中
            ZipEntry entry = new ZipEntry(name + "\\" + file.getName());
            zos.putNextEntry(entry);
           	//读取文件中的数据，写到压缩包
            FileInputStream fis = new FileInputStream(file);
            int b;
            while((b = fis.read()) != -1){
                zos.write(b);
            }
            fis.close();
            zos.closeEntry();
        }else{
            //4.判断-文件夹，递归
            toZip(file,zos, name + "\\r + file.getName());
        }
    }
}
```

### 工具包

#### Commons_io

下载：[Commons IO – 下载 Apache Commons IO](https://commons.apache.org/io/download_io.cgi)

#### HuTool

官网：[Hutool🍬一个功能丰富且易用的Java工具库，涵盖了字符串、数字、集合、编码、日期、文件、IO、加密、数据库JDBC、JSON、HTTP客户端等功能。](https://www.hutool.cn/)

## 多线程&JUC

### 实现

多线程的第一种启动方式：
1．自己定义一个类继承Thread
2．重写run方法
3．创建子类的对象，并启动线程

```java
public class MyThread extends Thread{
    @Override
    public void run(）{
        //书写线程要执行代码
        for（int i=0;i<100;i++）{
            System.out.println(getName(）+"HelloWorld");
        }
    }
}

MyThread t1= new MyThread();
MyThread t2 = new MyThread();
t1.setName("线程1"）;
t2.setName（"线程2"）;
t1.start();
t2.start();
```

多线程的第二种启动方式：
1.自己定义一个类实现Runnable接口
2.重写里面的run方法
3.创建自己的类的对象
4.创建一个Thread类的对象，并开启线程

class 实现接口 `implements Runnable`

设置线程名字需要获取当前下线程的对象`Thread t=Thread.currentThread();` `t.getName()`

```java
//创建MyRun的对象
//表示多线程要执行的任务
MyRun mr = new MyRun();
//创建线程对象
Thread t1 = new Thread(mr);
Thread t2 = new Thread(mr);
//给线程设置名字
t1.setName("线程1");
t2.setName（"线程2"）;
7/开启线程
t1.start();
t2.start();
```

多线程的第三种实现方式：
特点：可以获取到多线程运行的结果
1.创建一个类MyCallable实现callable接口
2.重写call（是有返回值的，表示多线程运行的结果）
3.创建MyCallable的对象（表示多线程要执行的任务）
4.创建FutureTask的对象（作用管理多线程运行的结果）
5.创建Thread类的对象，并启动（表示线程）

```java
public class MyCallable implements Callable<Integer>{
    @Override
    public Integer call(） throws Exception {
        // code //
    }
}

//创建MyCallable的对象（表示多线程要执行的任务）
MyCallable mc = new MyCallable();
//创建FutureTask的对象（作用管理多线程运行的结果）
FutureTask<Integer> ft = new FutureTask<>(mc);
//创建线程的对象
Thread t1 = new Thread(ft);
//启动线程
t1.start();
//获取多线程运行的结果
Integer result = ft.get();
System.out.println(result);0
```

### 常用成员方法

| 方法名称                         | 说明                                    |
| -------------------------------- | --------------------------------------- |
| String getName()                 | 返回此线程的名称                        |
| void setName(String name)        | 设置线程的名字 (构造方法也可以设置名字) |
| staticc Thread currentThread()   | 获取当前线程的对象                      |
| static void sleep(long time)     | 让线程休眠指定的时间，单位为毫秒<br/>   |
| setPriority(int newPriority)     | 设置线程的优先级                        |
| final int getPriority()          | 获取线程的优先级                        |
| final void setDaemon(boolean on) | 设置为守护线程                          |
| public static void yield()       | 出让线程/礼让线程                       |
| public static void join()        | 插入线程/插队线程                       |

### 线程的生命周期

- 创建线程对象：新建

  `start()`

- 有执行资格，没有执行权：就绪

  抢到了cpu的执行权

- 有执行资格，有执行权：运行

  `run()`

  `sleep()`/`wait()`或其他阻塞方法

  - 没有执行资格，没有执行权

    阻塞

    `sleep()`时间到或阻塞结束后回到第二步：就绪

  执行完毕

- 程序死亡，变成垃圾

### 线程的状态

| 状态                    | 结果             |
| ----------------------- | ---------------- |
| 新建状态(NEW)           | 创建线程对象     |
| 就绪状态(RUNNABLE)      | start();         |
| 阻塞状态(BLOCKED)       | 无法获得锁对象   |
| 等待状态(WAITING)       | wait();          |
| 计时等待(TIMED_WAITING) | sleep();         |
| 结束状态(TERMINATED)    | 全部代码运行完毕 |



### 线程同步

#### synchronized

```
synchronized (MyRun.class) {}
```

在代码块加入了同步方法后，仅同时允许一个线程执行，不可多线程同时执行代码块

#### Lock

```java
public class MyRun implements Runnable{
    private static int count = 0;
    private static final Lock lock = new ReentrantLock();
    private final Thread t = Thread.currentThread();
    @Override
    public void run() {
        while (true) {
            try {
                // synchronized (MyRun.class) {
                lock.lock();
                if (count < 100) {
                    count++;
                    System.out.println(t.getName() + "第" + count + "张票");
                } else {
                    break;
                }
                Thread.sleep(100);
            } catch (InterruptedException e) {
                throw new RuntimeException(e);
            } finally {
                lock.unlock();
            }
        }
    }
}
```

### 等待唤醒机制

```
wait(); // 使线程等待
notify(); // 唤醒一个线程
notifyAll(); // 唤醒所有等待的线程
```

让一个线程`wait()`，然后通过`notify()`唤醒其他线程

### 阻塞队列

- BlockingQueue
  - ArrayBlockingQueue
  - LinkedBlockingQueue

等待唤醒机制需要在同一个队列中完成

### 线程池

| 方法名称                                                     | 说明                     |
| ------------------------------------------------------------ | ------------------------ |
| public static ExecutorService newCachedThreadPool()          | 创建一个没有上限的线程池 |
| public static ExecutorService newFixedThreadPool(int nThreads) | 创建有上限的线程池       |

`submit();`给线程池提交任务(run)

#### 自定义线程池

| 参数                 | 举例                                 | 范围                             |
| -------------------- | ------------------------------------ | -------------------------------- |
| 核心线程数量         | 3                                    | 不能小于θ                        |
| 最大线程数量         | 6                                    | 不能小于，最大数量>=核心线程数量 |
| 空闲线程最大存活时间 | 60                                   | 不能小于θ                        |
| 时间单位             | TimeUnit.SECONDS                     | 用TimeUnit指定                   |
| 任务队列             | new ArrayBlockingQueue<>(capacity:3) | 不能为null                       |
| 创建线程工厂         | Executors.defauLtThreadFactory()     | 不能为null                       |
| 任务的拒绝策略       | new ThreadPoolExecutor.AbortPolicy() | 不能为null                       |

有任务提交时，线程池会创建线程去执行任务，执行完毕归还线程
不断的提交任务，会有以下三个临界点：
当核心线程满时，再提交任务就会排队
当核心线程满队伍满时，会创建临时线程
当核心线程满队伍满临时线程满时，会触发任务拒绝策略

#### 获取最大并行数

```java
Runtime.getRuntime().availableProcessors();
```

#### 线程池多大合适

- CPU密集型运算

  计算多，文件访问少

  大小：最大并行数 + 1

- I/O密集型运算

  访问本地文件/数据库等多

  大小：最大并行数 * 期望CPU利用率 * 总时间(CPU计算时间 + 等待时间) / CPU计算时间

可以使用thread dump测量计算时间

#### 额外扩展

还没看。。。

## 网络编程

C/S：Client/Server(客户端/服务器)

B/S：Browser/Server

IP：设备在网络中的标识，是唯一的标识

端口号：应用程序在设备中唯一的标识

协议：数据在网络中传输的规则，常见的协议有UDP、TCP、http、https、ftp

### IP

IPv4：采用32位地址长度，分成4组，点分十进制表示法，2^32个，已经用完了

IPv6：采用128位地址长度，分成8组，冒分十六进制表示法，省略前面的0，0位压缩表示法，2^128个

**关于IPv4的一些小细节**

2019/11/26 IPv4已经被分配完毕了

公网IP（万维网）和私网IP（局域网）

192.168.是私网IP

节省IP：多个设备共用一个公网IP，分配不同的私网IP

特殊IP：127.0.0.1或localhost:，是回送地址也称本地回环地址，本机IP

常见CMD命令：`ipconfig`：查看本机IP，`ping`：检查网络是否连通

### InetAddress

| 方法名称                                  | 说明                                                         |
| ----------------------------------------- | ------------------------------------------------------------ |
| static InetAddress getByName(String host) | 确定主机名称的IP地址。主机名称可以是机器名称，也可以是IP地址 |
| String getHostName()                      | 获取此IP地址的主机名                                         |
| String getHostAddress()                   | 返回文本显示中的IP地址字符串                                 |

### 端口号

有两个字节表示的整数，取值范围：0~65535，0~1023别人用我们不能用，

一个端口号只能被一个应用程序使用

### 协议

计算机网络中，连接和通讯的规则被称为网络通讯协议

| OSI参考模型 | TCP/IP参考模型  | TCP/IP参考模型各层对应协议   | 面向哪些                               |
| ----------- | --------------- | ---------------------------- | -------------------------------------- |
| 应用层      | 应用层          | HTTP、 FTP、 Telnet、 DNS... | 把是应用程序需要关注的。               |
| 表示层      |                 |                              | 如浏览器，邮箱。程序员一般在这一层开发 |
| 会话层      |                 |                              |                                        |
| 传输层      | 传输层          | TCP、UDP...                  | 选择传输使用的TCP，UDP协议             |
| 网络层      | 网络层          | IP、 ICMP、 ARP...           | 封装自己的IP，对方的IP等信息           |
| 数据链路层  | 物理+数据链路层 | 硬件设备。                   | 转换成二进制利用物理设备传输           |
| 物理层      |                 | 010100101010100101010...     |                                        |

#### UDP协议

- 用户数据报协议
- UDP是面向无连接的通讯协议
- 速度快，有大小限制一次最多发送64K，数据不安全，易丢失数据
- 不管是否连接成功都发送数据

##### 发送数据

```java
//1.创建DatagramSocket对象（快递公司）
//细节：
//绑定端口，以后我们就是通过这个端口往外发送
//空参：所有可用的端口中随机一个进行使用
//有参：指定端口号进行绑定
DatagramSocket ds = new DatagramSocket();
//2.打包数据
String str="你好威啊！！！"；
byte[] bytes = str.getBytes();
InetAddress address = InetAddress.getByName("127.0.0.1");
int port = 10086;
DatagramPacket dp = new DatagramPacket(bytes, bytes.length, address, port);
//3.发送数据
ds.send(dp);
//4.释放资源
ds.close();
```

##### 接收数据

```java
//1.创建DatagramSocket对象（快递公司）
//细节：
//在接收的时候，一定要绑定端口
//而且绑定的端口一定要跟发送的端口保持一致
DatagramSocket ds = new DatagramSocket(10086);
//2.接收数据包
byte[] bytes = new byte[1024];
DatagramPacket dp = new DatagramPacket(bytes, bytes.length);
ds.receive(dp);
//3.解析数据包
byte[] data = dp.getData();
int len = dp.getLength();
InetAddress address = dp.getAddress();
int port = dp.getPort();

System.out.println("接收到数据" + new String(data, θ, len));
System.out.println("该数据是从" + address + "这台电脑中的" + port + "这个端口发出的");
//4.释放资源
ds.close();
```

##### 三种通信方式

**单播**

> 一对一

**组播**

> 一对多

组播地址： 224.0.0.0 ～ 239.255.255.255

224.0.0.0 ～ 224.0.0.255 为预留的组播地址

代码使用`MulticastSocke`

**广播**

> 一对所有

广播地址：255.255.255.255

代码与单播相同，地址不同

#### TCP协议

- 传输控制协议TCP
- TCP是面向连接的通讯协议
- 速度慢，没有大小限制，数据安全
- 确保连接成功后才发送数据

```java
// TCPSend
Socket socket = new Socket("127.0.0.1", 10000);

OutputStream os = socket.getOutputStream();
os.write("你好".getBytes());

os.close();
socket.close();

// TCPReceive
ServerSocket serverSocket = new ServerSocket(10000);

Socket socket = serverSocket.accept();

InputStream inputStream = socket.getInputStream();
InputStreamReader inputStreamReader = new InputStreamReader(inputStream);
BufferedReader bufferedReader = new BufferedReader(inputStreamReader);

int b;
while ((b = bufferedReader.read()) != -1) {
    System.out.print((char)b);
}

socket.close();
serverSocket.close();
```

**TCP通信程序**

三次握手(确保链接建立)

客户端向服务器发送请求，服务器向客户端返回请求，客户端向服务器再发出确认信息

四次挥手(确保链接断开，且数据处理完毕)

客户端发送取消连接请求，服务器向客户端返回请求，服务器数据处理完毕后向客户端发送确认取消连接信息，客户端再发送确认信息



## 反射

> 反射允许对封装类的字段，方法和构造函数的信息进行编程访问。

### 获取CLass对象

- `CLass.getName("全类名")`
- `类名.class`
- `对象.getClass.()`

### 利用反射获取构造方法

| 方法名称                                                     | 说明                           |
| ------------------------------------------------------------ | ------------------------------ |
| Constructor<?>[] getConstructors()                           | 返回所有公共构造方法对象的数组 |
| Constructor<?>[] getDeclaredConstructors()                   | 返回所有构造方法对象的数组     |
| Constructor<T> getConstructor(Class<?>... parameterTypes)    | 返回单个公共构造方法对象       |
| Constructor<T> getDeclaredConstructor(Class<?>... parameterTypes) | 返回单个构造方法对象           |

Constructor类中用于创建对象的方法

| 方法名称                         | 说明                        |
| -------------------------------- | --------------------------- |
| T newlnstance(Object...initargs) | 根据指定的构造方法创建对象  |
| setAccessible(boolean flag)      | 设置为true,表示取消访问检查 |

### 利用反射获取成员变量

| 方法名称                            | 说明                           |
| ----------------------------------- | ------------------------------ |
| Field[] getFields()                 | 返回所有公共成员变量对象的数组 |
| Field[] getDeclaredFields()         | 返回所有成员变量对象的数组     |
| Field getField(String name)         | 返回单个公共成员变量对象       |
| Field getDeclaredField(String name) | 返回单个成员变量对象           |

Field类中用于创建对象的方法

| 方法名称                           | 说明   |
| ---------------------------------- | ------ |
| void set(Object obj, Object value) | 赋值   |
| Object get(Object obj)             | 获取值 |

### 利用反射获取成员方法

| 方法名称                                                     | 说明                                       |
| ------------------------------------------------------------ | ------------------------------------------ |
| Method[] getMethods()                                        | 返回所有公共成员方法对象的数组，包括继承的 |
| Method[] getDeclaredMethods()                                | 返回所有成员方法对象的数组，不包括继承的   |
| Method getMethod(String name, Class<?>... parameterTypes)    | 返回单个公共成员方法对象                   |
| Method getDeclaredMethod(String name, Class<?>... parameterTypes) | 返回单个成员方法对象                       |

Method类中用于创建对象的方法

`Object invoke(Object obj, Object... args)`：运行方法

参数一：用obj对象调用该方法
参数二：调用方法的传递的参数 (如果没有就不写)
返回值：方法的返回值 (如果没有就不写)

## 动态代理

> 无侵入式的给代码增加额外的功能

### Proxy类
