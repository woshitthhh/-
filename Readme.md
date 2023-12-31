# 十大排序算法

## 冒泡排序

**最优时间复杂度：**O(n)（数组元素都是有序的）

**最坏时间复杂度：**O(n^2) （数组元素都是倒序，每次都要交换）

**平均时间复杂度：**O(n^2)（数组元素都是无序的）

1. 循环实现

   ```cpp
   void BubbleSort1(int *arr, int n)
   {
       if (n < 2)
           return;
       int i, j, temp;
       for (i = 0; i < n - 1; i++)
       {
           for (j = 0; j < n - i - 1; j++)
           {
               if (*(arr + j) > *(arr + j + 1))
               {
                   Swap(arr + j, arr + j + 1); //交换元素
               }
           }
       }
   }
   ```

2. 递归实现

   ```cpp
   void BubbleSort2(int *arr, int n)
   {
       if(n < 2) 
           return;
       int i, temp;
       for(i = 0; i < n-1; i++)
       {
           if(*(arr + i) > *(arr + i + 1))
           {
               Swap(arr + i, arr + i + 1); //交换元素
           }
       }
       BubbleSort2(arr, --n);
   }
   ```

注：Swap函数如下定义：

```cpp
void Swap(int *a, int *b)
{
    int temp = *a;
    *a = *b;
    *b = temp;
}
```

冒泡排序的优化：如果进行i次排序后，数组已经有序，原始的冒泡排序还要继续比较下去，浪费时间，则可采用下列优化的冒泡排序：

1. 循环实现

   ```cpp
   void BubbleSort1(int *arr, int n)
   {
       if (n < 2)
           return;
       int i, j, temp;
       for (i = 0; i < n - 1; i++)
       {
           int ifSwap = 0; //设置一个ifSwap变量，记录是否发生过元素交换
           for (j = 0; j < n - i - 1; j++)
           {
               if (*(arr + j) > *(arr + j + 1))
               {
                   Swap(arr + j, arr + j + 1);
                   ifSwap = 1;
               }
           }
           if (!ifSwap) //如果没发生元素交换，说明前面的n-i个元素都是有序的，跳出循环
               break;
       }
   }
   ```

2. 递归实现：

   ```cpp
   void BubbleSort2(int *arr, int n)
   {
       if (n < 2)
           return;
       int i, temp, ifSwap = 0; //设置一个ifSwap变量，记录是否发生过元素交换
       for (i = 0; i < n - 1; i++)
       {
           if (*(arr + i) > *(arr + i + 1))
           {
               Swap(arr + i, arr + i + 1);
               ifSwap++;
           }
       }
       cout << n <<endl;
       if (!ifSwap) //如果没发生元素交换，说明前面的n-i个元素都是有序的，不用继续递归
           return;
       BubbleSort2(arr, --n);
   }
   ```

   