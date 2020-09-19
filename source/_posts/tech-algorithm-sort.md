---
title: 排序算法
date: 2020-08-13 19:34:10
tags:
---

> 更新中(づ￣ 3￣)づ

## 算法简介
一个算法的评价主要从**时间复杂度**和**空间复杂度**来考虑，

### 时间复杂度
我们把问题的规模称为n，（这个n代表着要处理的数量）
>一般情况下，算法中基本操作重复执行的次数是问题规模  n  的某个函数 f(n) ，算法的时间度量记作  T(n)=O(f(n))  表示随着问题规模  n  的增大，算法执行时间的增长率和  f(n)  的增长率相同，称作算法的渐进时间复杂度，简称时间复杂度。

比如冒泡排序，时间复杂度就是T(n)=n^2（因为有两层循环）

### 空间复杂度
空间复杂度是指算法占用内存空间的值

> 正餐开始( •̀ ω •́ )✧

## 冒泡排序

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

## 选择排序

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
## 插入排序
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

## 希尔排序
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

## 快速排序

### 思想

基本思想是：通过一趟排序将要排序的数据分割成独立的两部分，其中一部分的所有数据都比另外一部分的所有数据都要小，然后再按此方法对这两部分数据分别进行快速排序，整个排序过程可以递归进行，以此达到整个数据变成有序序列。

### 示例代码

```java
    public static int partition(int arr[], int low, int high) {
        int i=low, j=high, pivot=arr[low];
        while(i<j) {
            while(i<j && arr[j]>pivot) // 从右向左扫描，直到找到一个数小于pivot的
                j--;

            if(i<j) {                  // arr[i]和arr[j]交换后，i右移一位
                int temp=arr[i];
                arr[i]=arr[j];
                arr[j]=temp;
                i++;
            }

            while(i<j && arr[i]<=pivot)// 从左往右扫描
                i++;

            if(i<j) {                  // arr[i]和arr[j]交换后，j左移一位
                int temp=arr[i];
                arr[i]=arr[j];
                arr[j]=temp;
                j--;
            }
        }
        // 返回最终划分完成后基准元素所在位置
        return i;
    }

    public static void quick_sort(int arr[], int low, int high) {
        int mid;
        if(low<high) {
            mid = partition(arr, low, high);// 进行分割操作并返回基准元素
            quick_sort(arr, low, mid-1);    // 左区间递归快速排序
            quick_sort(arr, mid+1, high);   // 右区间递归快速排序
        }
    }

    public static void quick_sort(int arr[], int n) {
        quick_sort(arr, 0, n-1);
    }
```

给👴整懵逼了，这段代码中，找到中间那个数 是重点，就是这个数前面的都是比它小的，后面的都是比它大的