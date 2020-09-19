---
title:  算法-概述
date: 2020-06-22 23:08:04
tags:
categories: 算法
---

## 简介
算法是指解题方案的准确而完整的描述，是一系列解决问题的清晰指令，算法代表着用系统的方法描述解决问题的策略机制。
> 算法五个重要的特征：
> 1. 有穷性
> 2. 确定性(无二义)
> 3. 可(能)行性 
> 4. 输入
> 5. 输出 

一个算法的评价主要从**时间复杂度**和**空间复杂度**来考虑，

## 时间复杂度
我们把问题的规模称为n，（这个n代表着要处理的数量）
>一般情况下，算法中基本操作重复执行的次数是问题规模  n  的某个函数 f(n) ，算法的时间度量记作  T(n)=O(f(n))  表示随着问题规模  n  的增大，算法执行时间的增长率和  f(n)  的增长率相同，称作算法的渐进时间复杂度，简称时间复杂度。

比如冒泡排序：
```java
  /**
     * 冒泡排序
     */
    public static void bubble_sort(int array[]){
        System.out.println("冒泡排序开始");
        for(int i=0;i<array.length-1;i++){//在这里会循环n次
            for(int j=i+1;j<array.length;j++){//在这里又会循环n次
                if(array[j]>array[i]){
                    int temp=array[j];
                    array[j]=array[i];
                    array[i]=temp;
                }
            }
        }//所以时间复杂度就是T(n)=n^2啦
        System.out.println(Arrays.toString(array));
        System.out.println("冒泡排序结束");
    }
```


## 空间复杂度
空间复杂度是指算法占用内存空间的值