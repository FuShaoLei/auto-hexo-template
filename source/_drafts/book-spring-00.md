---
title: Spring-简介
date: 2020-06-22 22:12:09
tags:
categories: Spring
---

## IoC和DI的概念

- IoC：控制反转（设计原则）`由容器主动将资源推送到它所管理的组件里，组件要有接受资源的方式`
- DI：依赖注入（IoC的典型实现

## 3种配置元数据的方法

### 基于Xml的配置

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:context="http://www.springframework.org/schema/context"
	xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-4.0.xsd
		http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-4.0.xsd">
	<!-- id写什么都行 只要保证唯一就行，在Spring容器中用id来调用-->
	<!--  class要写完整路径,Spring运行时通过class这个路径来实例化对象放入Spring容器中 -->
	<bean id="InteCpu" class="com.pc.InteCpu"></bean>
	<bean id="Computer" class="com.pc.Computer">
	<!-- name要写Computer中的类名名称 -->
	<!-- ref依赖注入，ref里写id -->
	<property name="cpu" ref="InteCpu"></property>
	</bean>
</beans>
```
然后引用：
```java
package com.pc;

import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class Test {
	public static void main(String[] args) {
		//接口
		ApplicationContext ctx=new ClassPathXmlApplicationContext("applicationContext.xml");
		Computer pc=(Computer)ctx.getBean("Computer");//从Spring容器内调用id为Computer的类（？不知是否改用这个词）
		pc.play();//运行
	}
}
```

### 基于注解的配置

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:context="http://www.springframework.org/schema/context"
	xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-4.0.xsd
		http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-4.0.xsd">
	<!-- 用注解的方式 -->
	<context:annotation-config/>
	<!-- 说明包在哪，然后就会帮你扫描com.pc下所有的类
	当扫描到@Component的时候，则会帮你把这个"组件"实例化出来放入
	Spring容器中（自动分配的id首字母是小写的），当扫描到@Resource的时候，说明要依赖注入，Spring会自动帮你引入依赖-->
	<context:component-scan base-package="com.pc">
	</context:component-scan>
</beans>
```
比如：
```java
package com.pc;
import javax.annotation.Resource;
import org.springframework.stereotype.Component;
/**
 * 配置元数据第二种方法：基于注解的配置
 */
@Component("Computer")
public class Computer {
	//加入这个标签，说明
	@Resource
	private Cpu cpu;

	public void setCpu(Cpu cpu) {
		this.cpu = cpu;
	}
	public void play() {
		this.cpu.run();
		System.out.println("computer is playing by annotation");
	}
}
```
引用的方法和`基于Xml的配置`的差不多

### 基于Java的配置

此方法没有xml文件，纯java引用
```java
package com.pc;
import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.support.ClassPathXmlApplicationContext;

@Configuration
@ComponentScan("com.pc")
public class Test {
	public static void main(String[] args) {
		//接口
		ApplicationContext ctx=new AnnotationConfigApplicationContext(Test.class);
		Computer pc=(Computer)ctx.getBean("Computer");
		pc.play();
	}
}
```

需要添加注解，此方法可以理解为另一种形式的`基于注解的配置`

> 当扫描到@Component的时候，则会帮你把这个"组件"实例化出来放入
Spring容器中（自动分配的id首字母是小写的），当扫描到@Resource的时候，说明要依赖注入，Spring会自动帮你引入依赖