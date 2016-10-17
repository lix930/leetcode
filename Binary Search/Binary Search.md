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
