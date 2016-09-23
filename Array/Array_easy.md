## 121. Best Time to Buy and Sell Stock
**问题描述**
Say you have an array for which the ith element is the price of a given stock on day i.

If you were only permitted to complete at most one transaction (ie, buy one and sell one share of the stock), design an algorithm to find the maximum profit.

**Example 1:**
```
Input: [7, 1, 5, 3, 6, 4]
Output: 5

max. difference = 6-1 = 5 (not 7-1 = 6, as selling price needs to be larger than buying price)
```
 **Example 2:**

```
Input: [7, 6, 4, 3, 1]
Output: 0

In this case, no transaction is done, i.e. max profit = 0.
```
----------
**解法**

这题如果使用2个for循环 会超时 

```java
public class Solution {
    public int maxProfit(int[] prices) {
        int maxprofit = 0;
        for (int i=prices.length-1; i>=0; i--){
            for(int j =0; j<i; j++){
                int profit = prices[i] - prices[j];
                if(profit > maxprofit)
                    maxprofit = profit;
            }
        }
        return maxprofit;
    }
}
```
 AC代码如下
```java
public class Solution {
    public int maxProfit(int[] prices) {
        if(prices == null || prices.length==0)
            return 0;
        int maxProfit = 0;
        int curMin = prices[0];
        
        for(int curPrice : prices) {
            curMin = Math.min(curMin, curPrice); //储存当前价格最小值
            maxProfit = Math.max(maxProfit, curPrice-curMin); //最大利润=当前价格-已知的最小价格
        }
        return maxProfit;
    }
}
```


##  217. Contains Duplicate
**问题描述**
Given an array of integers, find if the array contains any duplicates. Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.
**解法**
```java
public class Solution { //使用HashSet O(N)
    public boolean containsDuplicate(int[] nums) {
        final Set<Integer> set = new HashSet<Integer>();
        for(int num : nums){
            if(set.contains(num))
                return true;
            set.add(num);
        }
        return false;
    }
}
```

```java
public class Solution { //   O(NlgN)
    public boolean containsDuplicate(int[] nums) {
        Arrays.sort(nums);
        for(int i=1; i<nums.length; i++){
            if(nums[i] == nums[i-1])
                return true;
        }
        return false;
    }
}
```


## 219. Contains Duplicate II
**描述**
Given an array of integers and an integer k, find out whether there are two distinct indices i and j in the array such that nums[i] = nums[j] and the difference between i and j is at most k.

**解法**
```java
public boolean containsNearbyDuplicate(int[] nums, int k) { //用HashSet
  if(nums.length <=1)
    return false;
  Set<Integer> set = new HashSet<Integer>();
  for(int i = 0; i < nums.length; i++){
    if(i>k)
      set.remove(nums[i-k-1]);
    if(!set.add(nums[i])) //如果set.add时 set中有相同的值，就会返回false
      return true;
  }
  return false;
}
```

```java
public boolean containsNearbyDuplicate(int[] nums, int k) { //用HashMap
  	if(nums.length <=1)
   	 	return false;
    Map<Integer, Integer> map = new HashMap<Integer, Integer>();
    for (int i = 0; i < nums.length; i++) {
        if (map.containsKey(nums[i])) {
            if (i - map.get(nums[i]) <= k) return true;
        }
        map.put(nums[i], i);
    }
    return false;
}
```



## 169. Majority Element


Given an array of size *n*, find the majority element. The majority element is the element that appears **more than** `⌊ n/2 ⌋` times.

You may assume that the array is non-empty and the majority element always exist in the array.

找出现次数最多的项

```java
public class Solution {
    public int majorityElement(int[] nums) {
        Map<Integer, Integer> map = new HashMap<Integer, Integer>();
        for(int i = 0; i < nums.length; i++){ //遍历数据，用HashMap计数
            if(!map.containsKey(nums[i]))
                map.put(nums[i],1);
            else
                map.put(nums[i], map.get(nums[i]) + 1);
        }
        int key = nums[0];
        int majority = Integer.MIN_VALUE;
        for(int i = 0; i<nums.length; i++){  //遍历数据，找出出现次数最多的值
            if(map.get(nums[i]) > majority){
                majority = map.get(nums[i]);
                key = nums[i];
            }
                
        }
        return key;
    }
}
```




## 18. Merge Sorted Array


Given two sorted integer arrays *nums1* and *nums2*, merge *nums2* into *nums1* as one sorted array.

**Note:**
You may assume that *nums1* has enough space (size that is greater or equal to *m* + *n*) to hold additional elements from *nums2*. The number of elements initialized in *nums1* and *nums2* are *m* and *n* respectively.

合并两个排好序的数组。 假设nums1足够大，则可以合并的时候从nums1的后端开始。



```java
public void merge(int[] nums1, int m, int[] nums2, int n) {
    int index = m + n - 1;
    int p1 = m-1;
    int p2 = n-1;
    while(index >= 0){
        if(p1<0)
            nums1[index--] = nums2[p2--];  //p1减完后，复制剩余的nums2到nums1
        else if(p2<0)
          	return;
            //nums1[index--] = nums1[p1--];  //p2减完后，复制剩余的num1到nums1 这里可以改为return;
            //或不写
        else
            nums1[index--] = (nums1[p1] > nums2[p2] ? nums1[p1--] : nums2[p2--]);
    }
}
```

## 396. Rotate Function

Given an array of integers `A` and let *n* to be its length.

Assume `Bk` to be an array obtained by rotating the array `A` *k* positions clock-wise, we define a "rotation function" `F` on `A` as follow:

`F(k) = 0 * Bk[0] + 1 * Bk[1] + ... + (n-1) * Bk[n-1]`.

Calculate the maximum value of `F(0), F(1), ..., F(n-1)`.

**Note:**
*n* is guaranteed to be less than 10^5.

**Example:**

```
A = [4, 3, 2, 6]

F(0) = (0 * 4) + (1 * 3) + (2 * 2) + (3 * 6) = 0 + 3 + 4 + 18 = 25
F(1) = (0 * 6) + (1 * 4) + (2 * 3) + (3 * 2) = 0 + 4 + 6 + 6 = 16
F(2) = (0 * 2) + (1 * 6) + (2 * 4) + (3 * 3) = 0 + 6 + 8 + 9 = 23
F(3) = (0 * 3) + (1 * 2) + (2 * 6) + (3 * 4) = 0 + 2 + 12 + 12 = 26

So the maximum value of F(0), F(1), F(2), F(3) is F(3) = 26.
```