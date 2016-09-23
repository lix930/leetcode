## 136. Single Number

Given an array of integers, every element appears *twice* except for one. Find that single one.

**Note:**
Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

第一眼看到这题目的解法： 用 HashMap 计数， 然后找出计数为1的数；

```java
    public int singleNumber(int[] nums) {
    Map<Integer, Integer> map = new HashMap<>();
    int index = 0;
    for(int i = 0; i < nums.length; i++){
        if(map.containsKey(nums[i]))
            map.put(nums[i], map.get(nums[i]) + 1);
        else
            map.put(nums[i], 1);
    }
    for(int i = 0; i < nums.length; i++){
        if(map.get(nums[i]) == 1)
            index = i;
    }
    return nums[index];
}
```
trick solutions

```java
public int singleNumber(int[] nums) {
        int res = 0;
        for(int num : nums) {
            res ^= num;   //使用 异或
        }
        return res;
    }
```

XOR 操作符 的特性

1. xor是可交换顺序的运算符 （i.e. `a xor b = b xor a`）
2. 一个数 异或 自己等于0 （i.e. `a xor a = 0`）
3. `0 xor a = a`

即    `a xor b xor a = a xor a xor b = 0 xor b = b.` 

`[1,4,1,4,5]` ->`1 xor 4 xor 1 xor 4 xor 5`  -> `1 xor 1 xor 4 xor 4 xor 5` -> `0 xor 0 oxr 5 `  -> `5`

