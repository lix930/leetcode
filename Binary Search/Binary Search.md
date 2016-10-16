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