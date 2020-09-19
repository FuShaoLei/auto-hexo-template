---
title: JavaSE
date: 2020-06-29 12:01:21
tags:
categories: 专业课
---

## 〇，简介
Java是由Sun公司于1995年5月推出的面向对象程序设计语言和Java平台的总称

## 一，基础语法

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

- 整型：`byte`,`short`,`int`,`long`
- 浮点型：`float`,`double`
- 字符型：`char`
- 布尔类型:`boolean`

<!--more-->
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

## 二，面向对象

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