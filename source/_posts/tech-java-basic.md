---
title: Java基础
date: 2020-08-04 11:32:08
tags:
---

## 基础语法
> 简介：Java是由Sun公司于1995年5月推出的面向对象程序设计语言和Java平台的总称

### 基本结构

```java
/**
 * Java程序的基本结构
 * @author sorryfu
 */
public class Hello {//class表示这是一个类，Hello则是这个类的类名
	public static void main(String[] args) {//main方法是程序的入口
		System.out.println("Hello World");//执行的语句
	}
}

```

### 输入/输出
输入`System.in`，输出`System.out`
#### 输入
需借助`Scanner`对象读取`System.in`的输入
示例：

```java
import java.util.Scanner;

public class Hello {
	public static void main(String[] args) {
		Scanner input=new Scanner(System.in);
		System.out.println("请输入一个数字");
		int num=input.nextInt();
		System.out.println("你输入的数字是："+num);
	}
}

```
#### 输出
```java
System.out.println("Hi");
System.out.print("Hi");
System.out.printf("Hi");
```

### 基本数据类型


基本类型 | 位数 | 字节 | 默认值 |对应的包装器类
--|--|--|--|--
`int` | 32 |4 | 0 | `Integer`
`short`|16|2|0 | `Short`
`long`|64 |8 |0L | `Long`
`byte`| 8 |1 |0 | `Byte`
`char`|16|2|'u0000' | `Character`
`float` | 32 |4 |0f | `Float`
`double`|64 |8 |0d|`Double`
`boolean`|1 | |false |`Boolean`

> 注意:
1. Java 里使用`long`类型的数据一定要在数值后面加上**L**，否则将作为整型解析
2. char a = 'h'char :单引号，String a = "hello" ：双引号

### 变量与常量

#### 变量
- 可以反复赋值
- 定义变量：`变量类型`（可用`var`代替）+`变量名`=`初始值`

#### 常量
- 定义初始化后不可以再次赋值
- 定义常量：变量前加一个`final`修饰符
> 常量名通常全部大写,例如：`final int PINUM=3.14`

### 整数运算

- 除：`/`
- 取余：`%` (获得余数)
- 自增/自减：`++`/`--`
  - `++n`/`--n`：先`+`/`-` 1再引用`n`
  - `n++`/`n--`：先引用`n`再`+`/`-` 1
- 移位运算：

```java
int n = 7;       // 00000000 00000000 00000000 00000111 = 7
int a = n << 1;  // 00000000 00000000 00000000 00001110 = 14
int b = n >> 1;  // 00000000 00000000 00000000 00000011 = 3
```
- 位运算
  - 与：`&`，都为1结果才为1
  - 或：`|`，任意一个为1结果就为1
  - 非：`~`，一元运算符，例如`~0=1` , `~1=0`
  - 异或：`^`,两个数不同时为1，例如`n=0^1`为1

#### 运算优先级，从高到低依次是

- `( )`
- `!` `~` `++` `--`
- `*` `/` `%`
- `+` `-`
- `<<`  `>>` `>>>`
- `&`
- `|`
- `+=` `-=` `*=` `/=`

#### 类型自动提升与强制转型
- 如参与运算的两个数类型不一致，则结果为较大类型的整型
- 强制转换：(有时候会得到错误的结果)
```java
int i=12345;
short s =(short)i;
```

### 流程控制
#### 条件分支流程
普通分支语句
```java
int a=1;
int b=2;
if(a>b){
System.out.println("a大于b")//如果a大于b则执行这个语句
}else if(a==b){
System.out.println("a等于b")//如果a等于b则执行这个语句
}esle{
System.out.println("a小于b")//否则就a小于b，当以上两种情况都不是的时候执行
}
```
条件多分支语句
```java
		int g=2;
		switch(g) {
		case 1:{
			System.out.println("是1");//当g是1时执行
			break;
		}
		case 2:{
			System.out.println("是2");//当g是2时执行
			break;
		}
		default:{
			System.out.println("都不是");//当以上情况都不是的时候执行
			break;
		}
		}
```


#### 循环流程
根据条件，反复执行某些操作
##### `for`
```java
	for(int i=0;i<5;i++) {//int i=0是初始值，i<5是循环条件。i++是循环后更新i的值，然后进入下一轮循环
		System.out.println("循环第"+i+"次");
	}
```


##### `while`
```java
		int u=5;
		while(u>0) {//当为true时执行
			System.out.println("u="+u);
			--u;
		}
```


##### `do`..`while`
```java
		int p=0;
		do {//无条件进入循环
			++p;
			System.out.println("p="+p);
		}while(p<5);//首先执行一次循环体后进行判断，若为true则继续进行下去
```

##### 增强型`for`
```java
for ( 类型 变量名: 数组或集合 ) {
循环体
}

```

### 数组
存储一组具有**相同数据类型**的数据元素的有序集合

#### 一维数组
##### 声明
```java
int num[];
int[] sum;
```
##### 初始化
> 未初始化就不能使用

###### 静态初始化
```java
int num[]={1,2,3,4,5}
```
###### 动态初始化
```java
int num[]=new int[5];//预先分配内存空间
for(int i=0;i<5;i++){
	num[i]=i*3;
}
```
#### 二维数组
##### 声明
```java
int[][] array1;
int[] array2[];
int array3[][];
```
###### 静态初始化
```java
int num[][]={{1,2},{3,4}}
```
###### 动态初始化
```java
int num[][]=new int[3][2];//预先分配内存空间
for(int i=0;i<3;i++){
	for(int j=0;j<2;j++){
		num[i][j]=i+2;
	}
}
for(int i=0;i<3;i++){
	System.out.println("第"+i+"个是");
	for(int j=0;j<2;j++){
		System.out.println(num[i][j]); 
	}
}
```

## 面向对象

> 面向对象的大三特性就是封装 继承 多态了，下面逐一进行理解
推荐阅读：[面向对象编程三大特性------封装、继承、多态](https://blog.csdn.net/jianyuerensheng/article/details/51602015)


### 基础知识

**面向对象编程**，是一种通过**对象**的方式，把**现实世界映射到计算机模型**的一种编程方法。

- 方法重载：指多个方法的方法名相同，但各自的参数不同；

### 封装

1. 封装是把一个**对象的属性私有化，同时提供一些可以被外界访问的属性的方法**（例如常见的getter setter方法）
2. 特性（好处）：
	- 实现信息隐藏
	- 隐藏了具体实现细节
	- 使某些成员设为私有从而提高了安全性和可靠性。

### 继承
1. 继承是指**当A类继承B类时（关键字`extends`），A类就自动获得B类的所有功能**，体现了代码的复用性。
2. 但是，**子类无法访问父类的`private`字段或方法**，这时候只需把`private`改成`protected`就好，对于`protected`而言，它指明就类用户而言，他是`private`，**但是对于任何继承与此类的子类而言或者其他任何位于同一个包的类而言，他却是可以访问的。**
3. **子类不会继承任何父类的方法**，这是必须用`super()`（有可能会有参数），来去**调用父类**的构造方法
4. **向上转型**（这里理解的不是很透彻。。），把一个子类类型安全地变为父类类型的赋值，例如`Person p = new Student();//Student/继承自Person，当这样操作时，Student会自动向上转型为Person（这里不太理解。。）`

### 多态
1. **针对某个类型的方法调用，其真正执行的方法取决于运行时期实际类型的方法**
2. 这个是真滴不太理解。。(╯‵□′)╯︵┻━┻

## 抽象类和接口

### 抽象类
> 关键字：`abstract`

```java
//定义一个抽象类
public abstract class Animal {
    //可在抽抽象类中定义方法，需要在抽象类中实现
    public void sleep(){
        System.out.println("睡觉");
    }
    //也可定义一个抽象方法，继承这个抽象类必须要实现这个抽象方法
    public abstract void eat();
}

```
```java
//继承抽象类，则必须实现这个抽象方法
public class Cat extends Animal{
    //实现抽象类中的方法
    @Override
    public void eat() {
        System.out.println("我喜欢恰鱼");
    }
}
```
```java
public class Test {
    public static void main(String[] args) {
        Animal cat=new Cat();
        cat.sleep();//可用抽象类中内置的方法
        cat.eat();//也可用继承抽象类后实现的抽象方法
    }
}
```

### 接口
> 关键字 ：`interface`

```java
//定义一个接口类
public interface Eat {
    void i_can_eat();//定义一个接口方法
}
```
```java
//实现这个接口类（非继承）
public class Cat implements Eat {
    @Override
    public void i_can_eat() {
        System.out.println("我可以吃鱼~");
    }
}
```
```java
public class Test {
    public static void main(String[] args) {
        Cat cat=new Cat();
        cat.i_can_eat();
    }
}
```

### 两者的区别
- 最大的一个区别：就是`interface`中只能定义方法，而不能有方法的实现，而在`abstract class`中则可以既有方法的具体实现，又有没有具体实现的抽象方法
- 一个类只能有一个继承类，但可以实现多个接口

## 枚举

> 这东西给我的感觉就像一个数组一样，只能用里面定义的东西

```java
public class Test {
    //定义一个枚举类
    enum People{MAN,WOMAN}
    public static void main(String[] args) {
        //枚举就是在一个类里定义几个静态变量，每个变量都是这个类的实例。
        People people=People.MAN;//实例化
        switch (people){
            case MAN:{
                System.out.println("我是一个男滴");
                break;
            }
            case WOMAN:{
                System.out.println("我是一个女滴");
                break;
            }
        }
    }
}
```

## 异常

![](https://cdn.jsdelivr.net/gh/fushaolei/img2/20200716223838.jpg)

> 对于异常java提供了两种常见的解决方式
- 捕获异常
- 抛出异常

### 捕获异常
```java
try {
    //接受监视的程序块,在此区域内发生的异常,
}catch (Exception e){//要处理的异常种类和标识符
    e.printStackTrace();//处理异常
}//如果想捕获多个异常，加入多个catch语句即可
```

> 在catch后还可以加入`finally`语句，这是一个总被执行的代码块，可用来回收资源等

### 抛出异常
>一个方法不处理它产生的异常,而是沿着调用层次向上传递，由调用它的方法来处理这些异常，叫抛出异常。

```java
throw (异常对象)
```

## 字符串

### 基本概念
定义：n个字符组成的序列
#### 初始化
```java
        //两种初始化方法
        String name1="xiaoming";
        String name2=new String("xiaogang");
```
> Sting类是final的，无法被继承

#### 字符串类
- 字符串常量类
 - `java.lang.String`
- 字符串变量类
 - `java.lang.StringBuffer`
 - `java.lang.StringBuilder`
- 字符串分隔解析类
 - `java.util.StringTokenizer`


### `StringBuffer`
> 字符串变量类

- StringBuffer对象的值可以修改
- 主要用于对字符串做大量修改的操作时

### `StringBuider`

StringBuilder类与StringBuffer类的方法调用是一致的。

#### 区别：
- StringBuffer是线程安全的
- StringBuilder是非线程安全的

## 容器和泛型

### 容器
> 也可叫集合类
### `List`
> 关心的是索引

- 对象按索引存储
- 可以存储重复元素
- 具有与索引相关的一套方法

实现类

- `ArrayList`：动态数组
 - 快速迭代，少量插入删除
- `LinkedList`：链表
 - 迭代速度慢，快速插入删除

#### `Set`
> 最简单的几何，关心唯一性

- 对象无序存储
- 不能存储重复的元素

实现类

- `HashSet`
- `LinkedHashSet`
- `TreeSet`

#### `Queue`
> 只允许在表的前端（front，队头）进行删除操作，而在表的后端（rear，队尾）进行插入操作

#### `Map`

- 对象以键－值对（key-value）存储
- key不允许有重复，value允许有重复

实现类

- `HashMap` 非线程安全
- `TreeMap`
- `LinkedHashMap`

### 泛型
> 为了提高代码的重用性，用通用的数据类型Object来实现

- Java 中的泛型只接受引用类型作为类型参数。