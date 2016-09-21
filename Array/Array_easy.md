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

Given an array of integers, find if the array contains any duplicates. Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.
有3种解法
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