[TOC]

> 作者：阿程 
>
> vx同qq：1764930806

# 冒泡排序（bubbleSort）

## 单向冒泡

###### 冒泡排序算法的基本思想

>将第一个元素和第二个元素进行比较，若为逆序则将两个元素交换，然后比较第二个元素和第三个元素。依次类推，直至第 n-1个元素和第 n个元素进行比较为止。上述过程称为第一趟冒泡排序，其结果使最大值元素被放置在最后一个位置（第 n个位置）。然后进行第二趟冒泡排序，对前 n-1个元素进行同样操作，其结果是使第二大元素被放置在倒数第二个位置上（第 n-1个位置）。

###### 冒泡排序图解

![在这里插入图片描述](C:\Users\Administrator\Documents\maopao.gif)

###### 代码实现

```java
import java.util.Arrays;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        /*输入一串数组*/
        System.out.println("输入数字并用,隔开");
        String str = sc.nextLine().toString();
        String[] arr = str.split(",");
        int[] b = new int[arr.length];
        for(int i = 0;i < b.length;i++){
            b[i] = Integer.parseInt(arr[i]);
        }
        /*结束输入*/
        bubbleSort(b); //引用冒泡排序对数组进行排序
        System.out.println(Arrays.toString(b)); //输出数组
    }
    /*冒泡排序 内外部均已优化 已达单向最优*/
    public static int[] bubbleSort(int[] arr){
        if(arr == null | arr.length <2){ //判断数组个数小于两个则直接返回
            return arr;
        }
        /*定义数组元素最后发生交换的位置*/
        int lastExchangeIndex = 0;      
        int sortBorder = arr.length-1;
        /*也可不定义使用如下方式替代
         for(int j = 0;j < arr.length-1-i;j++)*/

        for(int i =0;i < arr.length-1;i++) {
            boolean isSorted = true;//如果一趟中发生了数组交换代表无序则定义一个boolean变量使其判断是否有序 无交换则有序可以break循环了
            for(int j = 0;j < sortBorder;j++)
            {
                if(arr[j] > arr[j+1])//元素交换
                {
                    isSorted = false;
                    int tmp = arr[j];
                    arr[j] = arr[j+1];
                    arr[j+1] = tmp;
                    lastExchangeIndex = j;
                }
            }
            sortBorder = lastExchangeIndex;
            if(isSorted)
            {break;}
        }
        return arr;
    }
}
```

###### 代码性能测试

```java
import java.util.Date;


public class Main {
    public static void main(String[] args) {
        int[] b = new int[80000];
        for(int i = 0;i < b.length;i++)
        {
            b[i] = (int) (Math.random() * 80000); //随机生成80000个数
        }

        Date date1 = new Date();//使用Date函数进行打印时间
        System.out.println("使用冒泡算法前的时间："+date1);
        bubbleSort(b);
        Date date2 = new Date();
        System.out.println("使用冒泡算法后的时间："+date2);

    }
    public static int[] bubbleSort(int[] arr){
        if(arr == null | arr.length <2){
            return arr;
        }
        for(int i =0;i < arr.length-1;i++) {
            boolean isSorted = true;
            for(int j = 0;j < arr.length-1-i;j++)
            {
                if(arr[j] > arr[j+1])
                {
                    isSorted = false;
                    int tmp = arr[j];
                    arr[j] = arr[j+1];
                    arr[j+1] = tmp;
                }
            }
            if(isSorted)
            {break;}
        }
        return arr;
    }
}
```

![image-20220507132929046](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220507132929046.png)

> ps:对80000个数进行排序大概进行了10秒左右的时间，这个时间和每个电脑还有软件使用的不同有所差异。

## 双向冒泡

###### 双向思想

> 在很多时候，遍历的过程可以从两端进行，从而提升效率。因此在冒泡排序中，其实也可以进行双向循环，正向循环把最大元素移动到数组末尾，逆向循环把最小元素移动到数组首部。该种排序方式也叫双向冒泡排序，也叫鸡尾酒排序。

```java
import java.util.Arrays;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        /*输入一串数组*/
        System.out.println("输入数字并用,隔开");
        String str = sc.nextLine().toString();
        String[] arr = str.split(",");
        int[] b = new int[arr.length];
        for(int i = 0;i < b.length;i++){
            b[i] = Integer.parseInt(arr[i]);
        }
        /*结束输入*/
        bubbleSort(b); //引用冒泡排序对数组进行排序
        System.out.println(Arrays.toString(b)); //输出数组
    }
    static void bubbleSort(int[] arr){
        int len = arr.length;

        int preIndex = 0;
        int backIndex = len - 1;
        while(preIndex < backIndex){
            preSort(arr,len,preIndex);
            preIndex++;
            if(preIndex >= backIndex){
                break;
            }
            backSort(arr,backIndex);
            backIndex--;
        }
    }
    static void preSort(int[] arr,int len,int preIndex){
        for(int i = preIndex+1;i < len;i++){
            if(arr[preIndex] > arr[i]){
                swap(arr,i,preIndex);
            }
        }
    }
    static void backSort(int[] arr,int backIndex){
        for(int i = backIndex-1;i > 0;i--){
            if(arr[i] > arr[backIndex]){
                swap(arr,i,backIndex);
            }
        }
    }
    static void swap(int[] arr,int i,int j)
    {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
}

```

###### 代码测试

```java
import java.util.Date;
public class Main {
    public static void main(String[] args) {
        int[] b = new int[80000];
        for(int i = 0;i < b.length;i++)
        {
            b[i] = (int) (Math.random() * 80000); //随机生成80000个数
        }

        Date date1 = new Date();//使用Date函数进行打印时间
        System.out.println("使用冒泡算法前的时间："+date1);
        bubbleSort(b);
        Date date2 = new Date();
        System.out.println("使用冒泡算法后的时间："+date2);
    }
    static void bubbleSort(int[] arr){
        int len = arr.length;

        int preIndex = 0;
        int backIndex = len - 1;
        while(preIndex < backIndex){
            preSort(arr,len,preIndex);
            preIndex++;
            if(preIndex >= backIndex){
                break;
            }
            backSort(arr,backIndex);
            backIndex--;
        }
    }
    static void preSort(int[] arr,int len,int preIndex){
        for(int i = preIndex+1;i < len;i++){
            if(arr[preIndex] > arr[i]){
                swap(arr,i,preIndex);
            }
        }
    }
    static void backSort(int[] arr,int backIndex){
        for(int i = backIndex-1;i > 0;i--){
            if(arr[i] > arr[backIndex]){
                swap(arr,i,backIndex);
            }
        }
    }
    static void swap(int[] arr,int i,int j)
    {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
}

```

![image-20220507140526891](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220507140526891.png)

> 对80000个数进行排序大概进行了6秒左右的时间,比单向排序明显节约了很多时间
