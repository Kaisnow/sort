# 基本排序学习

[TOC]




## 冒泡排序

#### 算法原理



对于一组包含n个数据的记录，冒泡排序在最坏的情况下需要进行n-1趟排序

- 第1趟：依次比较0和1、1和2、2和3...（n-2）和（n-1）索引的元素，如果发现第1个数据大于第2个数据，交换他们，经过第1趟排序，最大的元素排到了最后
- 第2趟：依次比较0和1、1和2、2和3...（n-3）和（n-3）索引的元素，如果发现第1个数据大于第2个数据，交换他们，经过第2趟排序，第二大的元素排到了倒数第二个位置
- ...
- 第n-1趟：比较0和1索引的元素，如果发现第1个数据大于第2个数据，交换他们，经过第n-1趟排序，第二小的元素排到了第二个位置

#### 图示

​	![](https://github.com/Kaisnow/gitskiils/blob/master/img/7789414-9c7908de122ee2d6.gif?raw=true)





#### 代码实现



~~~java
        public static void bubble_Sort(int [] array){
        for (int i=0;i<array.length-1;i++){
            boolean key = true;
            for (int j=0;j<array.length-i-1;j++) {
                if (array[j] > array[j + 1]) {
                    key=false;
                    int temp = array[j];
                    array[j] = array[j + 1];
                    array[j + 1] = temp;

                }
            }
            //算法优化，如果当前一轮便利没有交换元素，说明已经形成有序序列；
          //算法优化，如果当前一轮便利没有交换元素，说明已经形成有序序列；
            // 此情况最优时间复杂度为O（n） i=0时，j变量for循环一遍结束；
            //最坏情况序列为反序  时间复杂度 O（n^2） 
            if (key==true)break;
        }
        print_List(array);
    }
~~~

#### 时间复杂度

| 排序类别 |   时间复杂度   （平均，最好最坏   | 空间复杂度 | 稳定性  | 复杂性  |
| ---- | :------------------: | :---: | ---- | ---- |
| 交换排序 | O(N2)   O(N2)   O(N) | O(1)  | 稳定   | 简单   |

#### 算法稳定性

冒泡排序就是把小的元素往前调或者把大的元素往后调。比较是相邻的两个元素比较，交换也发生在这两个元素之间。

所以相同元素的前后顺序并没有改变，所以冒泡排序是一种**稳定排序算法**。

#### 代码优化

如果进行**某一趟排序时并没有进行数据交换，则说明所有数据已经有序**，可立即结束排序，避免不必要的比较过程。



## 插入排序



#### 算法原理

在讲解直接插入排序之前，先让我们脑补一下我们打牌的过程。

先拿一张5在手里，

再摸到一张4，比5小，插到5前面，

摸到一张6，嗯，比5大，插到5后面，

摸到一张8，比6大，插到6后面，

。。。

最后一看，我靠，凑到全是同花顺，这下牛逼大了。 

![img](img/318837-20160422101457913-263070230.png)

以上的过程，其实就是典型的**直接插入排序，每次将一个新数据插入到有序队列中的合适位置里**。

很简单吧，接下来，我们要将这个算法转化为编程语言。

假设有一组无序序列 R0, R1, ... , RN-1。

(1) 我们先将这个序列中下标为 0 的元素R0当作元素个数为 1 的有序序列。

(2) 然后，我们要依次把 R1, R2, ... , RN-1 插入到这个有序序列中。所以，我们需要一个**外部循环**，从下标 1 扫描到 N-1 。

(3) 接下来描述插入过程。假设这是要将 Ri 插入到前面有序的序列中。由前面所述，我们可知，插入Ri时，前 i-1 个数肯定已经是有序了。

所以我们需要将Ri 和R0 ~ Ri-1 进行比较，确定要插入的合适位置。这就需要一个**内部循环**，我们一般是从后往前比较，即从下标 i-1 开始向 0 进行扫描。 





#### 图示

![](https://github.com/Kaisnow/gitskiils/blob/master/img/7789414-d3e7769cd797534d.gif?raw=true)





#### 



#### 代码实现

~~~java
   public static void insert_Sort(int [] array){
        //从第二个元素开始插入，并且插入到已排序完成序列中指定位置
         for (int i=1;i<array.length;i++){
             //当前准备插入的元素
             int temp = array[i];
             int j;
             //0到i-1都是从小到大已经排好的有序数列，
             // 如果比插入元素大就后移一位给插入元素让出插入位置，
             // 直到当前元素不大于插入元素  插入元素就插入在当前元素后一位
             //参考打扑克牌摸牌插入手法
             for (j=i-1;j>=0 && temp<array[j];j--){
                 array[j+1]=array[j];
             }
             //插入
             array[j+1]=temp;
         }
        print_List(array);
    }
~~~





#### 时间复杂度

| **排序类别 ** | **排序方法** | 时间复杂度   （平均，最好最坏  ) | **空间复杂度** | **稳定性** | **复杂性** |
| --------- | -------- | :-----------------: | --------- | ------- | ------- |
| 插入排序      | 直接插入排序   |   O(N2)O(N2) O(N)   | O(1)      | 稳定      | 简单      |



#### 算法稳定性

直接插入排序的过程中，不需要改变相等数值元素的位置，所以它是**稳定的**算法。



## 快速排序

#### 算法原理

- 从数列中挑出一个元素，称为 "基准"（pivot），

- 重新排序数列，所有元素比基准值小的摆放在基准前面，所有元素比基准值大的摆在基准的后面（相同的数可以到任一边）。在这个分区退出之后，该基准就处于数列的中间位置。这个称为**分区（partition）**操作。

- [递归](http://zh.wikipedia.org/wiki/%E9%80%92%E5%BD%92)地（recursive）把小于基准值元素的子数列和大于基准值元素的子数列排序。

- 排序前:    1  3  4  5  2  6  9  7  8  0 

  base = 1: 0  1  4  5  2  6  9  7  8  3 

  base = 4:       3  2  4  6  9  7  8  5 

  base = 3:       2  3 

  base = 6:                5  6  7  8  9 

  base = 7:                      7  8  9 

  base = 8:                         8  9 

  排序后:    0  1  2  3  4  5  6  7  8  9 

#### 图示

![](https://github.com/Kaisnow/gitskiils/blob/master/img/Sorting_quicksort_anim.gif?raw=true)









#### 代码实现

~~~java
public int division(int[] list, int left, int right) {
    // 以最左边的数(left)为基准
    int base = list[left];
    while (left < right) {
        // 从序列右端开始，向左遍历，直到找到小于base的数
       //千万不要忘记加等于不然死循环  
        while (left < right && list[right] >= base)
            right--;
        // 找到了比base小的元素，将这个元素放到left位置
        list[left] = list[right];
 
        // 从序列左端开始，向右遍历，直到找到大于base的数
        while (left < right && list[left] <= base)
            left++;
        // 找到了比base大的元素，将这个元素放到right位置
        list[right] = list[left];
    }
 
    // 最后将base放到left位置。此时，left位置的左侧数值应该都比left小；
    // 而left位置的右侧数值应该都比left大。
    list[left] = base;
    return left;
}
 
private void quickSort(int[] list, int left, int right) {
 
 	 
    if (left < right) {
      // 对数组进行分割，并且base左边小于base右边大于base
        int base = division(list, left, right);
 
        // 对“基准标号“左侧的一组数值进行递归的切割，以至于将这些数值完整的排序
        quickSort(list, left, base - 1);
 
        // 对“基准标号“右侧的一组数值进行递归的切割，以至于将这些数值完整的排序
        quickSort(list, base + 1, right);
    }
}
~~~



#### 时间复杂度

| **排序类别** | 时间复杂度   （平均，最好最坏  )           | **空间复杂度** | **稳定性** | **复杂性** |
| -------- | ----------------------------- | --------- | ------- | ------- |
| 交换排序     | O(Nlog2N)   O(N2)   O(Nlog2N) | O(Nlog2N) | 不稳定     | 较复杂     |

# 

​    

​       **递归算法的时间复杂度公式：T[n] = aT[n/b] + f(n)  ；**

**最优情况下时间复杂度**

​     快速排序最优的情况就是每一次取到的元素都刚好平分整个数组  此时的时间复杂度公式则为：**T[n] = 2T[n/2] + f(n)；T[n/2]为平分后的子数组的时间复杂度，f[n] 为平分这个数组时所花的时间；**下面来推算下，在最优的情况下快速排序时间复杂度的计算(用迭代法)：

​	

   T[n] =  2T[n/2] + n                                                                     ----------------第一次递归 



​                 令：n = n/2        =  2 { 2 T[n/4] + (n/2) }  + n                                               ----------------第二次递归 

​                                            =  2^2 T[ n/ (2^2) ] + 2n 

  ......................................................................................               

​                 令：n = n/(2^2)   =  2^2  {  2 T[n/ (2^3) ]  + n/(2^2)}  +  2n                         ----------------第三次递归  

​                                            =  2^3 T[  n/ (2^3) ]  + 3n 

​                 ......................................................................................                         

​                 令：n = n/(  2^(m-1) )    =  2^m T[1]  + mn                                                  ----------------第m次递归(m次后结束) 

最后平分的不能再平分时，也就是说把公式一直往下跌倒，到最后得到T[1]时，说明这个公式已经迭代完了（T[1]是常量了）。

得到：T[n/ (2^m) ]  =  T[1]    ===>>   n = 2^m   ====>> m = logn； 

T[n] = 2^m T[1] + mn ；其中m = logn; 

T[n] = 2^(logn) T[1] + nlogn  =  n T[1] + nlogn  =  n + nlogn  ；其中n为元素个数 

又因为当n >=  2时：nlogn  >=  n  (也就是logn > 1)，所以取后面的 nlogn； 

综上所述：快速排序最优的情况下时间复杂度为：O( nlogn ) 



**最差情况下时间复杂度**

​        **最差的情况就是每一次取到的元素就是数组中最小/最大的，这种情况其实就是冒泡排序了(每一次都排好一个元素的顺序)**

 这种情况时间复杂度就好计算了，就是冒泡排序的时间复杂度：T[n] = n \* (n-1) = n^2 + n;

综上所述：快速排序最差的情况下时间复杂度为：O( n^2 )





#### 算法稳定性

在快速排序中，相等元素可能会因为分区而交换顺序，所以它是不稳定的算法。

 







## 选择排序

#### 算法原理

- 比较未排序区域的元素，选出最大或最小的元素放到排序区域。
- 一趟比较完成之后，再从剩下未排序的元素开始比较。
- 反复执行以上步骤，只到排序完成。

#### 图示

![](https://github.com/Kaisnow/gitskiils/blob/master/img/v2-f20b8898585b3ca03843d93ce2c35a68_b.gif?raw=true)













#### 代码实现

~~~java
    public static void select_Sort(int [] array) {
        for (int i=0;i<array.length-1;i++){
            int index=i;
            for (int j=i+1;j<array.length;j++){
                if (array[j]<array[index]){
                    index=j;
                }
            }
            int temp = array[index];
            array[index]=array[i];
            array[i]=temp;
        }
        print_List(array);
    }
~~~



#### 时间复杂度

| **排序类别** | 时间复杂度   （平均，最好最坏  )   | **空间复杂度** | **稳定性** | **复杂性** |
| -------- | --------------------- | --------- | ------- | ------- |
| 交换排序     | O(N2)   O(N2)   O(N2) | O(1)      | 不稳定     | 简单      |

举个例子，序列5 8 5 2 9， 我们知道第一遍选择第1个元素5会和2交换，那么原序列中2个5的相对前后顺序就被破坏了，所以选择排序不是一个稳定的排序算法

####  



## 希尔排序

#### 算法原理

希尔排序是记录按下标的一定增量分组，对每组使用直接插入排序算法排序；随着增量逐渐减少，每组包含的关键词越来越多，当增量减至1时，整个文件恰被分成一组，算法便终止。

#### 图示

![](https://github.com/Kaisnow/gitskiils/blob/master/img/20160518211420194.png?raw=true)





初始时，有一个大小为 10 的无序序列。

- **第一趟排序中**，我们不妨设 gap1 = N / 2 = 5，即相隔距离为 5 的元素组成一组，可以分为 5 组。

接下来，按照直接插入排序的方法对每个组进行排序。

- **第二趟排序中**，我们把上次的 gap 缩小一半，即 gap2 = gap1 / 2 = 2 (取整数)。这样每相隔距离为 2 的元素组成一组，可以分为 2 组。

按照直接插入排序的方法对每个组进行排序。

- **第三趟排序中**，再次把 gap 缩小一半，即gap3 = gap2 / 2 = 1。 这样相隔距离为 1 的元素组成一组，即只有一组。按照直接插入排序的方法对每个组进行排序。此时，排序已经结束。



需要注意一下的是，图中有两个相等数值的元素 **5** 和 **5** 。我们可以清楚的看到，在排序过程中，**两个元素位置交换了**。

所以，希尔排序是不稳定的算法。



#### 代码实现

```java
public static void shell_Sort(int [] array) {
    //进行分组
    for (int gap=array.length/2;gap>0;gap/=2){
        //i=gap表示 从每组的第二个元素开始进行插入排序
      //插入排序每组第一个都不需要排序  所以从gap开始
        for (int i = gap ;i< array.length;i++){

            int temp = array[i];
            int j;
            // j-=gap  表示只和自己组比较
          for (j=i-gap;j>=0 && array[j]>temp ; j-=gap){   				//注意是 j+gap
                    array[j+gap]=array[j];
            }
            //注意是 j+gap
            array[j+gap]=temp;

        }
    }
    print_List(array);
}
```

#### 时间复杂度

| **排序类别** | 时间复杂度   （平均，最好最坏  )    | **空间复杂度** | **稳定性** | **复杂性** |
| -------- | ---------------------- | --------- | ------- | ------- |
| 插入排序     | O(Nlog2N)   未知 O(N1.5) | O(1)      | 不稳定     | 较复杂     |

####  



## 归并排序

#### 算法原理

归并排序的核心思想是将两个有序的数列合并成一个大的有序的序列。通过递归，层层合并，即为归并。

#### 图示

![](https://github.com/Kaisnow/gitskiils/blob/master/img/v2-a29c0dd0186d1f8cef3c5ebdedf3e5a3_b.gif?raw=true)





 



#### 代码实现

```java
   public static void merger_Sort(int [] array,int left , int right) {
        if (left>=right)return;

            //分而治之
            int mid = (left+right)/2;
            merger_Sort(array,left,mid);
            merger_Sort(array,mid+1,right);

           //分离的两边 比较并合并
         merge(array,left,mid,right);
    }

    public static void merge(int[] array, int left, int mid, int right) {
        int i = left;int j=mid+1;int k=0;
        //开辟新数组暂时存放
        int array2[] = new int[right-left+1];
        while (i<=mid && j<=right){
            //array[i]<=array[j]   不加=符号  此排序就不是稳定的
            if (array[i]<=array[j]){
                array2[k++]=array[i];
                i++;
            }else {
                array2[k++]=array[j];
                j++;
            }
        }
        while (i<=mid){
            array2[k++]=array[i++];
        }
        while (j<=right){
            array2[k++]=array[j++];
        }
        //当前left-right 区间已经排序完成 复制到原数组对应部分
        for (k=0,i=left;i<=right;i++,k++){
            array[i]=array2[k];
        }
    }
```

#### 时间复杂度

| **排序类别** | 时间复杂度   （平均，最好最坏  ) | **空间复杂度** | **稳定性** | **复杂性** |
| -------- | ------------------- | --------- | ------- | ------- |
| 插入排序     | O(nlog2n)           | O(n)      | 稳定      | 较复杂     |

 **归并排序的形式就是一棵二叉树，它需要遍历的次数就是二叉树的深度，而根据完全二叉树的可以得出它的时间复杂度是O(n\*log2n)。**









