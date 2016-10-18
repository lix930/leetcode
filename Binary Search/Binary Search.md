## 35. Search Insert Position

Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You may assume no duplicates in the array.

Here are few examples.
`[1,3,5,6]`, 5 → 2
`[1,3,5,6]`, 2 → 1
`[1,3,5,6]`, 7 → 4
`[1,3,5,6]`, 0 → 0


solution: 二分查找类似
```java
public int searchInsert(int[] nums, int target) {  
    if(nums==null || nums.length==0)
        return 0;
    int start = 0;
    int end = nums.length - 1;
    int mid;
    while(start <= end){
        mid = (start + end) / 2;
        if(target < nums[mid])
            end = mid - 1;
        else if(target > nums[mid])
            start = mid + 1;
        else
            return mid;
    }
    return start;
}
```



## 74. Search a 2D Matrix

Write an efficient algorithm that searches for a value in an *m* x *n* matrix. This matrix has the following properties:

- Integers in each row are sorted from left to right.
- The first integer of each row is greater than the last integer of the previous row.

For example,

Consider the following matrix:

```
[
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
```

Given **target** = `3`, return `true`.



solution:

```java
public boolean searchMatrix(int[][] matrix, int target) {
    if(matrix == null || matrix.length == 0 || matrix[0].length == 0)
        return false;
    else{
        int m = matrix.length;
        int n = matrix[0].length;
        int row = 0;
        int col = n - 1;
        while(row < m && col >= 0){
            if(target < matrix[row][col])
                col--;
            else if(target > matrix[row][col])
                row++;
            else
                return true;
        }
        return false;
    }
}
```




## 140. Search a 2D Matrix II

与上一题解法一样

## 153. Find Minimum in Rotated Sorted Array

Suppose a sorted array is rotated at some pivot unknown to you beforehand.

(i.e., `0 1 2 4 5 6 7` might become `4 5 6 7 0 1 2`).

Find the minimum element.

You may assume no duplicate exists in the array.

solution:

首先处理边界条件，然后考虑一下条件

1. 如果rotate了，nums[min] < a[min - 1]

2. 如果没有，最小为nums[0]

   然后用二分查找

```java
public int findMin(int[] nums) {
    if(nums == null || nums.length == 0)
        return 0;
    else{
        if(nums.length == 1)
            return nums[0];
        int start = 0;
        int end = nums.length - 1;
        int mid;
        while(start < end){
            mid = (start + end) >>> 1;
            if (mid > 0 && nums[mid] < nums[mid - 1]) {
                return nums[mid];
            }
            if (nums[start] <= nums[mid] && nums[mid] > nums[end]) {
                start = mid + 1;
            } else {
                end = mid - 1;
            }
        }
        return nums[start];
    }
}
```



## 162. Find Peak Element

A peak element is an element that is greater than its neighbors.

Given an input array where `num[i] ≠ num[i+1]`, find a peak element and return its index.

The array may contain multiple peaks, in that case return the index to any one of the peaks is fine.

You may imagine that `num[-1] = num[n] = -∞`.

For example, in array `[1, 2, 3, 1]`, 3 is a peak element and your function should return the index number 2.

**Note:**Your solution should be in logarithmic complexity.

solution：

1. 遍历查找
2.  二分查找

```java
public int findPeakElement(int[] nums) {
    if(nums == null || nums.length == 0)
        return 0;
    else{
        int i;
        if(nums.length==1)
            return 0;
        if(nums[0]>nums[1])  //首
            return 0;
        for(i = 1; i < nums.length - 1; i++){
            if((nums[i] > nums[i-1]) && (nums[i] > nums[i+1])) //找到极大值
                return i;
        }
        if(nums[nums.length-1] > nums[nums.length-2]){ //尾
            return nums.length-1;
        }
        return 0;
    }
}
```