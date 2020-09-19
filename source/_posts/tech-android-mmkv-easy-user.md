---
title: MMKV的简单使用
date: 2020-07-08 23:39:46
tags:
categories: Android
---
## 简介
MMKV是腾讯的一个开源工具，可用于android或者ios平台，作用类似sharepreferences，（也是以键值对来存储数据的），但性能比sharepreferences好太多了。

贴一个github地址：https://github.com/Tencent/MMKV
## 使用方法

### 一，初始化
在`onCreate()`方法中，
```java
        String rootDir=MMKV.initialize(this);//初始化
        Log.i("MMKV", "mmkv root: " + rootDir);//打印一下
```
### 二，全局对象
```java
MMKV kv=MMKV.defaultMMKV();
```
>事实上，这里应该分开写，在全局里`private MMKV kv;`
>然后在`onCreate()`方法的`MMKV.initialize(this)`初始化后，才能进行`kv=MMKV.defaultMMKV();`
>

### 三，简单使用
> 以键值对存储嘛，操作起来也很简单

#### 存储
```java
kv.encode("name","小明");
```
#### 使用
```java
String getname=kv.decodeString("name");//对应不同类型，有不同的方法，但前面都是decode
```
#### 删除
```java
kv.removeValueForKey("name");
```
#### 显示所有
```java
kv.allKeys();//这里会返回一个String数组
```
