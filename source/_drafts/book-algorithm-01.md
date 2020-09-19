---
title: 排序算法
date: 2020-06-22 23:08:09
tags:
categories: 算法
---
## 一，冒泡排序

### 思想
**依次比较两个相邻的元素，如果他们的顺序错误就把他们的值互换**

### 示例代码

1. 两层循环
2. 依据需求比较互换

```java
    /**
     * 冒泡排序
     */
    public static void bubble_sort(int array[]){
        System.out.println("冒泡排序开始");
        for(int i=0;i<array.length-1;i++){
            for(int j=i+1;j<array.length;j++){
                if(array[j]>array[i]){
                    int temp=array[j];
                    array[j]=array[i];
                    array[i]=temp;
                }
            }
        }
        System.out.println(Arrays.toString(array));
        System.out.println("冒泡排序结束");
    }
```

## 二，选择排序

### 思想
**先假设比如第一个元素是最大的（或最小），然后去循环，如果有比它更大的元素，则互换**

### 示例代码

1. 假设最值
2. 比较互换

```java
    /**
     * 选择排序
     */
    public static void select_sort(int array[]){
        System.out.println("选择排序开始");
        int max;
        for(int i=0;i<array.length;i++){
            max=i;
            for (int j=i+1;j<array.length;j++){
                if (array[j]>array[max]){
                    max=j;
                }
            }
            int temp=array[i];
            array[i]=array[max];
            array[max]=temp;
        }
        System.out.println(Arrays.toString(array));
        System.out.println("选择排序结束");
    }
```
## 三，插入排序
> 这个稍微开始难理解了QAQ

### 思想
将无序区的第一个插入到有序区的适当位置
![](https://cdn.jsdelivr.net/gh/fushaolei/img/20200623105659.gif)

### 示例代码
```java
    /**
     * 插入排序
     */
    public static void insert_sort(int array[]){
        System.out.println("插入排序开始");
        int j,temp;
        for (int i=1;i<array.length;i++){
            temp=array[i];//选择第一个未排序的元素
            for(j=i-1;j>=0&&array[j]<temp;j--){
                //逆序遍历
                array[j+1]=array[j];//先右移
            }
            array[j+1]=temp;
        }
        System.out.println(Arrays.toString(array));
        System.out.println("插入排序结束");
    }
```

## 四，希尔排序
> 插入排序的优化版

### 思想
**按一定的增量分组，进行插入排序**
> 其实就是插入排序更加灵活的实现

### 示例代码
```java
    /**
     * 希尔排序
     */
    public static void shell_sort(int array[]){
        System.out.println("希尔排序开始");
        int i,j;
        int n=array.length;
        for (int d=n/2;d>0;d/=2){
            for (i=d;i<n;i++){
                int temp=array[i];
                for (j=i-d;j>=0&&temp<array[j];j-=d){
                    array[j+d]=array[j];
                }
                array[j+d]=temp;
            }
        }
        System.out.println(Arrays.toString(array));
        System.out.println("希尔排序结束");
    }
```

