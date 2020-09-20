---
title: 常用设计模式
date: 2020-08-13 19:33:06
tags:
---
> 选修课程笔记

## 什么是模式
> 重复出现的问题，它的通用的解决方案就是模式

### 是由三部分组成的规则
1. 特定的环境
2. 一个问题
3. 一个解决方案

本文在介绍每一个设计模式之前都会先说这三个部分

### 核心思想
设计的复用


### 面向对象原则

- 单一职责原则：高内聚低耦合（一个类完成一个职责，类和类之间的调用尽量少）
- 开闭原则：在不修改原有代码的基础上扩展其功能

### 好设计原则

- 依赖倒装原则：细节依赖抽象，针对接口编程
- 接口隔离原则：将一些大的接口细化成小的接口供客户端使用
- 合成复用原则：复用时尽量使用对象组合
- 迪米特法则：要求一个软件实体应当尽可能少的与其他实体发生相互作用

## 单例模式
确保一个类仅有一个**唯一的实例**（多次new只生成一个对象）
### 解决方法

1. private 私有化————在类外无法new出来了
2. static————控制全局只有一个
3. 提供一个获取实例的方法

## 观察者模式
> 又叫**发布-订阅**模式，我觉得还是这个名字好

### 介绍
- 背景：某对象发生了变化，需其他对象做出调整
- 两个角色：观察者和被观察者
- 当被观察者发生变化时，观察者回察到变化，并做出响应

类比的话 就像微信公众号一样，公众号若发布消息的话，所有订阅者都回收到消息，

### 实现
(A表示订阅者 B表示发布者)

1. 发布者将所有订阅者装进一个容器里
2. 发布者发布了某些信息，从容器中得到所有注册过的订阅者，将变化通知他。
3. 当订阅者不想订阅此发布者时，只需告知发布者，发布者即从容器中把此订阅者删除

> 下面是小小demo

```java
/**
 * 发布者，拥有以下几个功能
 * 1. 添加订阅者
 * 2. 删除订阅者
 * 3. 通知所有订阅者更新的信息
 */
public class Subject {
    private List<User> userList=new ArrayList<>();

    public void add(User weixinUser) {
        userList.add(weixinUser);
    }


    public void delete(User weixinUser) {
        userList.remove(weixinUser);
    }


    public void notify(String message) {
        for (User user:userList){//更新消息后 ，循环订阅者list，提醒更新
            user.update(message);
        }
    }
}

```
```java
/**
 * 订阅者
 */
public class User {
    private String name;

    public User(String name) {
        this.name = name;
    }


    public void update(String message) {
        System.out.println(name+" "+message);
    }
}

```
测试一下
```java
public class Test {
    public static void main(String[] args) {
        Subject subject=new Subject();
        User user1=new User("嘎嘎嘎");
        User user2=new User("咕咕咕");
        User user3=new User("嘻嘻嘻");

        //添加
        subject.add(user1);
        subject.add(user2);
        subject.add(user3);

        subject.notify("朕更新啦！");
        System.out.println("===================");
        //删除一个订阅者
        subject.delete(user2);
        subject.notify("朕又更新啦！");

    }
}

```

## 策略模式

### 介绍
> 可随时切换算法
> 策略模式定义了
一系列的算法，并将每一个算
法封装起来，而且使它们还可以相互替换。

### 实现
```java
/**
 * 一，定义一个抽象类
 */
public interface IStrategy {
    public void fighting();
}
```
```java
/**
 * 二，定义一些具体实现类
 */

/**
 * 技能一，冷箭
 */
public class Bow implements IStrategy {
    @Override
    public void fighting() {
        System.out.println("施冷箭");
    }
}
/**
 * 技能二，放炮
 */
public class Cannon implements IStrategy {
    @Override
    public void fighting() {
        System.out.println("开炮！");
    }
}
/**
 * 技能三，使刀
 */
public class Knife implements IStrategy {
    @Override
    public void fighting() {
        System.out.println("使刀中");
    }
}
```
```java
/**
 * 三，定义环境类
 */
public class Context {
    private IStrategy strategy;

    public Context() {
    }

    //为的是方便调用，方便转换
    public void setStrategy(IStrategy strategy) {
        this.strategy = strategy;
    }
    public void fight(){
        this.strategy.fighting();
    }
}
```
```java
/**
 * 测试
 */
public class Test {
    public static void main(String[] args) {
        Context context=new Context();
        context.setStrategy(new Bow());
        context.fight();
        context.setStrategy(new Cannon());
        context.fight();
        context.setStrategy(new Knife());
        context.fight();
    }
}
```

