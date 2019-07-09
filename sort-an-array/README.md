# [912. Sort an Array](https://leetcode-cn.com/problems/sort-an-array/)

### Description

Given an array of integers `nums`, sort the array in ascending order.



**Example 1:**

```
Input: [5,2,3,1]
Output: [1,2,3,5]
```

**Example 2:**

```
Input: [5,1,1,2,0,0]
Output: [0,0,1,1,2,5]
```

 

**Note:**

1. `1 <= A.length <= 10000`
2. `-50000 <= A[i] <= 50000`

<br>

### Solution 1

```java
// Merge Sort

class Solution {
    public int[] sortArray(int[] arr) {
        int []temp = new int[arr.length];	// 在排序前，先建好一个长度等于原数组长度的临时数组，避免递归中频繁开辟空间
        sort(arr,0,arr.length-1,temp);
        return arr;
    }
    
    private static int[] sort(int[] arr,int left,int right,int []temp){
        if(left<right){
            int mid = (left+right)/2;
            sort(arr,left,mid,temp);//左边归并排序，使得左子序列有序
            sort(arr,mid+1,right,temp);//右边归并排序，使得右子序列有序
            merge(arr,left,mid,right,temp);//将两个有序子数组合并操作

        }
        return arr;
    }
    private static void merge(int[] arr,int left,int mid,int right,int[] temp){
        int i = left;//左序列指针
        int j = mid+1;//右序列指针
        int t = 0;//临时数组指针
        while (i<=mid && j<=right){
            if(arr[i]<=arr[j]){
                temp[t++] = arr[i++];
            }else {
                temp[t++] = arr[j++];
            }
        }
        while(i<=mid){//将左边剩余元素填充进temp中
            temp[t++] = arr[i++];
        }
        while(j<=right){//将右序列剩余元素填充进temp中
            temp[t++] = arr[j++];
        }
        t = 0;
        //将temp中的元素全部拷贝到原数组中
        while(left <= right){
            arr[left++] = temp[t++];
        }
    }
    
}
```

<br>

### Solution 2

```java
// Quick Sort
class Solution {
    public int[] sortArray(int[] nums) {
        if (nums == null || nums.length == 0) return nums;
        quickSort(nums, 0, nums.length - 1);
        return nums;
    }

    private void quickSort(int[] nums, int start, int end) {
        if (start >= end) return;
        int i = start, j = end, pivot = nums[i + (j - i) / 2];
        while (i <= j) {
            while (i <= j && nums[i] < pivot) ++i;
            while (i <= j && nums[j] > pivot) --j;
            if (i <= j) {
                int tmp = nums[i];
                nums[i++] = nums[j];
                nums[j--] = tmp;
            }
        }
        quickSort(nums, i, end);
        quickSort(nums, start, j);
    }
}
```

<br>



### Note

- 像Bubble Sort，Select Sort，Insertion Sort这一类时间复杂度过高的，会超出时间限制，可用Quick Sort或者是Merge Sort