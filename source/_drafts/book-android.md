---
title: Android基础
date: 2020-06-23 20:21:00
tags:
categories: 专业课
---

## 〇，Android简介
一个操作系统
> Gradle 一个自动化建构工具 

Gradle
### LogCat
- Log.v ，任何消息都会输出
- Log.d，仅输出debug调试的意思
- Log.i，一般提示性的消息information 
- Log.w，可以看作为warning警告， 
- Log.e，可以显示红色的错误信息

## 一，用户界面基础
### 四大组件的作用
> 所有android应用都是由四大组件组成的：Activity，BroadcastReceiver，Service，ContentProvider

- Activity：最基本的组件，一个就是一个屏幕，通常都被实现为一个独立的类
- BroadcastReceiver：使用它对外部事件进行过滤，接收并做出响应
- Service：一个服务是具有一个较长生命周期且没有用户界面的程序。
- ContentProvider：使一个应用程序的指定数据集可以提供给其他应用程序。


### MVC模式
#### 基本概念
- M：Model：模型层，负责处理数据的加载或者存储
- V：View：视图层，负责界面数据的展示，与用户进行交互
- C：Controller：控制器层，负责逻辑业务的处理，处理用户数据

![](https://cdn.jsdelivr.net/gh/fushaolei/img/20200702093658.png)

#### 对应
- Model层对应了android中的数据库啊，文件的操作
- View层对应了android中的XML布局文件
- Controller层对应了Activity

事实上，Activity中的`setContentView`方法可以指定对应的布局，然后activity又可以操作数据说明的，这是视图层和控制器层甚至和Model层的结合

> 这种模式用起来真是混乱+冗余

### View类及子类
> View控件是界面的最基本的可视单元，是Android视图界面的基类。

![](https://cdn.jsdelivr.net/gh/fushaolei/img/20200702110528.png)


## 二，界面布局
### 创建布局的两种方法
#### 通过XML文件
1. 建立`XML`文件
2. 在`XML`文件中设置布局
3. 在Activity中设置布局（`setContentView`）
4. 如果是个`Activity`的话，还得在`AndroidManifest.xml`文件中进行添加
#### 通过Java代码
> 在`onCreate()`中进行操作

```jaVa
    @Override
    protected void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        //1.创建布局文件
        LinearLayout layout=new LinearLayout(this);//初始化
        //2.设置布局
        layout.setOrientation(LinearLayout.VERTICAL);//设置排列布局

        LinearLayout.LayoutParams params=new LinearLayout.LayoutParams(
                LinearLayout.LayoutParams.MATCH_PARENT,
                LinearLayout.LayoutParams.MATCH_PARENT
        );

        //3.创建视图控件
        TextView tv=new TextView(this);
        tv.setText("好麻烦啊这种方法");
        tv.setLayoutParams(params);

        layout.addView(tv);//将输入控件添加到layout布局里

        //4.为当前Activityu显示界面视图
        setContentView(layout);
        
        //5.去AndroidManifest.xml文件中进行注册

        //爷吐了 这个方法也太麻烦了
    }
```

### 线性布局
LinearLayout：按照水平或者垂直的顺序排列

属性名 | 可填 
--|--
`layout_with`<br>`layout_height` | `match_parent`：占满父容器<br>`wrap_content`：内容多少我就多少 
`orientation` | `vertical`：垂直布局<br>`horizontal`：水平布局 
`layout_weight` | 成比例分配空间 

### 相对布局
RelativeLayout：能够指定相对位置关系，是一种非常灵活的布局方式
特点：能够最大程度保证在各种屏幕类型的手机上正确显示界面布局

属性名 | 可填
--|--
`layout_alignParentTop`<br>`layout_alignParentBottom`<br/>`layout_alignParentLeft`<br/>`layout_alignParentRight`<br/>`layout_alignParentStart`<br/>`layout_alignParentEnd`<br/> |可以填`true` 或者`false`<br>看名字就知道了，表示在父元素的什么位置
`layout_toStartOf`<br>`layout_toEndOf`<br/>`layout_toLeftOf`<br/>`layout_toRightOf`<br/> |这里要填的是id<br>表示在这个id元素的什么位置

### 其他
> 这些没必要深入，知道就好

- TableLayout：表格布局
- GridLayout：网格布局
- FrameLayout：帧布局

## 三，高级组件
### AdapterView
这里就不展开了 之前写过一篇 [Listview学习]([https://sorryfu.top/2020/06/24/Listview%E5%AD%A6%E4%B9%A0/](https://sorryfu.top/2020/06/24/Listview学习/))
### TabHost
> 其实现在谁还用原生的tabhost啊？不过这是学校的基本课程，还是值得一学的
 fragment tabhost

#### 继承fragment类的配置
```java
public class FirstFragment extends Fragment {
    @Nullable
    @Override
    /**
     * onCreateView中的参数
     * LayoutInflater 布局填充其， 加载view文件
     * ViewGroup 父容器
     * Bundle 页面之间传递数据用的
     */
    public View onCreateView(@NonNull LayoutInflater inflater, @Nullable ViewGroup container, @Nullable Bundle savedInstanceState) {
        View view = inflater.inflate(R.layout.fragment_layout,//内容页面
                container,//根视图对象
                false );//false表示需要手动跳到用addView方法将view添加到container中
        //如果是true的话 表示不需要手动调用addView方法

        return view;
    }
}
```
就这个蛮重要，其他的我都不想鸟，太麻烦了
## 四，通知消息和菜单
### 三种通知消息
#### 对话框
#### Toast
一句话用法
```java
/**
 * 三个参数
 * 1.上下文
 * 2.提示的信息
 * 3.提示的时长（LONG/SHORT）
 */
Toast.makeText(getApplicationContext(),"提示的内容",Toast.LENGTH_LONG).show();
```
#### Notification

### 菜单

## 事件处理
监听器
回调方法
## 多线程
handler
子线程
异步
## Activity的创建和跳转
注册：步骤
跳转的原理，两种跳转方法
## Activity的生命周期
activity的生命周期
fragment的生命周期
## Intent的使用
概念
作用
## 待看
- listview部分
- handler机制部分