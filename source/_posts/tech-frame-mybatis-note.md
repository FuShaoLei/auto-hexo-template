---
title: MyBatis笔记
date: 2020-08-14 14:12:12
tags:
---

> 这框架是大三下学期的课程了，当时学的时候是用的eclipse的，现在换用IDEA 遇到了许多的坑，特此记录，然后，这也是个从零开始学mybatis的博文，为了期末考试，也为了巩固自己的编码基础，特写此文.
> **注：编码环境**
>
> -  IDEA 2020.1
> -  Mysql 8.0.20
> -  全部都是Maven项目（为方便引入jar包）
>
> 外加一个官网指路👉https://mybatis.org/mybatis-3/
>
> 还有一个自己学mybatis时敲过的全部代码：https://github.com/FuShaoLei/FrameDemo/tree/master/Mybatis



## 第一个项目
> 分为以下几步
> 1. 创建一个maven项目
> 2. 配置包，编译
> 3. 创建entity类，以及映射器接口和SQL映射XML文件
> 5. 创建mybatis的 xml配置文件并关联SQL映射XML文件
> 6. 测试
> 
> 👴哭了，第一次配置太麻烦了

### 导入jar包
由于我是maven项目，根据官方的文档 ，只需在pom.xml中添加相应的东西即可
```xml
<dependencies>
    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis</artifactId>
        <version>3.5.5</version>
    </dependency>
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>8.0.20</version>
    </dependency>
</dependencies>
```

### 从 XML 中构建 SqlSessionFactory

> **每个基于 MyBatis 的应用都是以一个 SqlSessionFactory 的实例为核心的。**SqlSessionFactory 的实例可以通过 SqlSessionFactoryBuilder 获得。而 SqlSessionFactoryBuilder 则可以从 XML 配置文件或一个预先配置的 Configuration 实例来构建出 SqlSessionFactory 实例。(官方原话)

由上面可知，要创建一个xml配置文件，为的是构建SqlSessionFactory实例。根据官方给的xml配置文件示例进行修改即可

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <settings>
        <setting name="logImpl" value="STDOUT_LOGGING" />
    </settings>
    <environments default="dev">
        <environment id="dev">
            <transactionManager type="JDBC" />
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.cj.jdbc.Driver" />
                <property name="url"
                          value="jdbc:mysql://localhost:3306/mybatis_db?useUnicode=true&amp;characterEncoding=utf-8&amp;serverTimezone=GMT" />
                <property name="username" value="root" />
                <property name="password" value="18389621811" />
            </dataSource>
        </environment>
    </environments>

    <mappers>
        <mapper resource="com/mapper/StudentMapper.xml"/>
    </mappers>
</configuration>
```
> 要注意的是那个name为url的value值，有name为driver的value值，mysql5.0和mysql8.0的配置不太一样！

好了到这里已经编写好了xml文件，接下来是构建SqlSessionFactory，根据老师的教学，编写MybatisUtil
```java
/**
 * 从 XML 中构建 SqlSessionFactory
 */
public class MybatisUtil {
    private static SqlSessionFactory sessionFactory;
    static {
        InputStream is;
        try {
            is= Resources.getResourceAsStream("mybatis-config.xml");
            sessionFactory = new SqlSessionFactoryBuilder().build(is);
        }catch (IOException e){
            e.printStackTrace();
        }
    }
    public static SqlSession getSession(){
        return sessionFactory.openSession();
    }
}
```
通过阅读以上代码可知，MybatisUtil这个类暴露了一个`getSession()`方法供使用这个`sessionFactory.openSession();`这个是什么意思呢？ 👴也不懂啊 woc


### 测试
然后就可以进行简单的测试了，具体看代码

在这里说个坑。

> 推荐阅读：https://blog.csdn.net/qq_23184291/article/details/78089115

算了 👴不想说了，反正就是要往pom.xml中添加

```xml
<build>
    <resources>
        <resource>
            <directory>src/main/java</directory>
            <includes>
                <include>**/*.xml</include>
            </includes>
        </resource>
    </resources>
</build>
```

## 简单的CRUD
> 随便贴些代码，具体还得看项目

映射器接口

```java
/**
 * 实现简单的CRUD
 */
public interface StudentMapper {
    //增
    public void insertStudentNoReturnId(Student student);
    public int insertStudentAndReturnId(Student student);
    //删
    public void deleteStudent(int id);
    //改
    public void updateStudent(String sex,int id);

    //查
    public List<Student> selectAllStudent();
    public Student selectStudent(int id);
}
```
SQL映射XML文件
```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.mapper.StudentMapper">
    <!--增-->
    <insert id="insertStudentNoReturnId">
        insert into students(name,sex) values (#{name},#{sex})
    </insert>
    <!--如果想在执行插入操作以后返回表中的主键值，需要在映射文件中insert元素中加上如下两个属性-->
    <insert id="insertStudentAndReturnId" useGeneratedKeys="true" keyProperty="id">
        insert into students(name,sex) values (#{name},#{sex})
        <selectKey resultType="int" keyProperty="id" order="AFTER">
            select last_insert_id()
        </selectKey>
    </insert>
    <!--删-->
    <delete id="deleteStudent">
        delete from students where id=#{id}
    </delete>
    <!--改-->
    <!--跟据id修改性别 (￣▽￣)"-->
    <update id="updateStudent">
        update students set sex=#{arg0} where id=#{arg1}
    </update>
    <!--查-->
    <select id="selectAllStudent" resultType="com.entity.Student">
        select * from students
    </select>
    <select id="selectStudent" resultType="com.entity.Student">
        select * from students where id = #{id}
    </select>
</mapper>
```

这里要说明的一点是，那个插入后放回的值不是id，二十它影响的行数，如果要获取id的话
（除了需要改动映射的xml文件），直接getId即可，如下
```java
int returnId = studentMapper.insertStudentAndReturnId(student2);
//插入后直接student2.getId()即可
System.out.println("影响的行数是：" + returnId+" 新插入的id是："+student2.getId());
```