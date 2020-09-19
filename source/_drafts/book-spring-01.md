---
title: IoC容器和Bean
date: 2020-06-22 23:03:57
tags:
categories: Spring
---

> 讲那么快  👴😭了

## BeanFactory
负责对`Bean`对象的实例化，装配和生命周期的管理
### 与`ApplicationContext`的联系与区别
#### 联系
`ApplicationContext`是`BeanFactory`的一个子接口
#### 区别
- `BeanFactory`提供了配置框架和基本功能，`ApplicationContext`是它的一个完整的超集
- `BeanFactory`直到`getBean()`方法调用时才被创建（慢载入`Bean`）
- `ApplicationContext`启动后载入所有的单列`Bean`

## Bean的实例化

### 通过构造方法
`id`保证唯一性，`class`里填完整路径
```xml
<bean id="InteCpu" class="com.pc.InteCpu"></bean>
```
### 使用静态工厂方法
在类中写静态方法，用静态方法来返回某一个类的对象,`factory-method`里写静态方法的名称
```xml
<bean id="Computer" class="com.pc.Computer" factory-method="createInstance"></bean>
```
### 使用实例工厂方法

这时则没有`class`属性，`factory-bean`来指定所要的`bean`名称,用`factory-method`来指定要用的方法
```xml
<bean id="Thinkpad" class="com.pc.Thinkpad"></bean>
<bean id="Computer" factory-bean="Thinkpad" factory-method="createComputer"></bean>
```
## Bean的依赖注入

### 方式

#### 1.构造器注入
- 注入值：`<constructor-arg value="xxx"></constructor-arg>`
- 注入方法：`<constructor-arg ref="xxx"></constructor-arg>`
> 还可以加入type index name这些属性

#### 2.`Setter`方法注入

自动调用`set`方法来进行注入
- 注入值：`<property name="xxx" value="xxx"></property>`
- 注入方法：`<property name="xxx" ref="xxx"></property>`

##### 基本Bean注入
- 注入List/Array
```xml
<property name=“xxx”>
<list>
<ref bean=“aa”/>
<ref bean=“bb” />
<value>aaa</value>
<value>bbb</value>
</list>
</property>
```
- 注入Set
```xml
<property name=“xxx”>
<set>
<value>java</value>
<value>c</value>
<value>java</value>
</set>
</property>
```
- 注入Map
```xml
<property name=“xxx”>
<map>
<entry key="a" value-ref="aa" />
<entry key="b" value-ref="bb" />
</map>
</property>
```
- 注入Properties
```xml
<property name=“xxx”>
<props>
<prop key="a">aaa</prop>
<prop key="b">bbb</prop>
</props>
</property>
```

> 🥤 Bean是一个由Spring IoC容器进行实例化、装配和管理的对象，
Beans以及他们之间的依赖关系是通过容器使用配置元数据反应出来的