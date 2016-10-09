##  171. Excel Sheet Column Number

Related to question [Excel Sheet Column Title](https://leetcode.com/problems/excel-sheet-column-title/)

Given a column title as appear in an Excel sheet, return its corresponding column number.

For example:

```
    A -> 1
    B -> 2
    C -> 3
    ...
    Z -> 26
    AA -> 27
    AB -> 28 
```

solution: 转化为26进制问题。

```java
public int titleToNumber(String s) {
  	int result = 0;
  	for (int i = s.length() - 1, j = 0; i >= 0; i--, j++)
   		result += Math.pow(26, j) * (s.charAt(i) - 'A' + 1);
 	return result;
    
}
```

看了别人的答案，发现可以不用Math.pow()

```java
public int titleToNumber(String s) {
    int result = 0;
    for(int i = 0 ; i < s.length(); i++) {
      result = result * 26 + (s.charAt(i) - 'A' + 1);
    }
    return result;
  }
```

##  126. Power of Three
Given an integer, write a function to determine if it is a power of three.

Follow up:
Could you do it without using any loop / recursion?

solution:

```java
public boolean isPowerOfThree(int n) {
    return (Math.log10(n) / Math.log10(3)) % 1 == 0;
}
```

## 263. Ugly Number

Write a program to check whether a given number is an ugly number.

Ugly numbers are positive numbers whose prime factors only include `2, 3, 5`. For example, `6, 8` are ugly while `14` is not ugly since it includes another prime factor `7`.

Note that `1` is typically treated as an ugly number.
solution: 分别整除2，3，5，看最后结果是否为1

```java
public boolean isUgly(int num) {
    if(num == 1)
        return true;
    if(num <= 0)
        return false;
    while( num % 2 == 0){
        num = num / 2;
    }
    while( num % 3 == 0)
        num = num / 3;
    while(num % 5 == 0)
        num = num / 5;
    if(num == 1)
        return true;
    else
        return false;
}
```