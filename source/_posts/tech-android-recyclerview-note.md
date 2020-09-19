---
title: RecyclerView入门笔记
date: 2020-06-24 15:38:51
categories: Android
---
> 进阶笔记，推荐阅读： [Android 控件 RecyclerView](https://www.jianshu.com/p/4f9591291365)

## 简介
RecyclerView是一个强大的控件，可用来替代Listview

## 基础
> 像使用listview一样使用它

### 1.添加依赖

```java
implementation 'androidx.recyclerview:recyclerview:1.0.0'
```
### 2. 准备数据

### 3. 创建Adapter
1. 创建一个类`MyAdapter`
2. 在这个类里再创建一个类（通常命名为`VH`）继承自`RecyclerView.ViewHolder`
3. 在VH里写item的控件
4. 让`MyAdapter`继承`RecyclerView.Adapter<MyAdapter.VH>`
5. 重写那三个方法

### 4. 绑定适配器
```java
        recyclerView.setLayoutManager(new LinearLayoutManager(this));
        recyclerView.setAdapter(new MyAdapter(studentArrayList));
```


## 进阶
