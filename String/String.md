## 412. Fizz Buzz

Write a program that outputs the string representation of numbers from 1 to n.

But for multiples of three it should output “Fizz” instead of the number and for the multiples of five output “Buzz”. 
For numbers which are multiples of both three and five output “FizzBuzz”.
solution: 很简单
```java
public List<String> fizzBuzz(int n) {
        List<String> result = new LinkedList<String>();
        for(int i = 1; i <= n; i++){
            if( (i % 3 == 0) && (i % 5 == 0) ){
                result.add("FizzBuzz");
            }
            else if( i % 3 == 0){
                result.add("Fizz");
            }
            else if( i % 5 == 0){
                result.add("Buzz");
            }
            else{
                result.add("" + i);
            }
        }
        return result;
    }
```


##  58. Length of Last Word

Given a string *s* consists of upper/lower-case alphabets and empty space characters `' '`, return the length of last word in the string.

If the last word does not exist, return 0.

**Note:** A word is defined as a character sequence consists of non-space characters only.

For example, 
Given *s* = `"Hello World"`,
return `5`.


```java
public int lengthOfLastWord(String s) {
    if(s == null || s.length() == 0)
        return 0;
    else{
        int i = s.length()-1;
        int count = 0;
        for(; i>=0 ; i--){
            if(s.charAt(i) == ' ')
                ;
            else{
                break;
            }
        }
        for(; i>=0; i--){
            if(s.charAt(i) == ' ')
                break;
            else
                count++;
        }
        return count;
    }
}
```



## 28. Implement strStr()

Implement strStr().

Returns the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

    public int strStr(String haystack, String needle) {
        int i = 0;
        int j = 0;
        while(i<haystack.length() && j<needle.length()){
            if(haystack.charAt(i) == needle.charAt(j)){
                i++;
                j++;
            }else{
                i = i - j + 1;
                j = 0;
            }
        }
        if(j == needle.length())
            return i - j;
        else
            return -1;
    }

## 344. Reverse String

Write a function that takes a string as input and returns the string reversed.

**Example:**
Given s = "hello", return "olleh".

solution: 使用递归的解法

```java
public String reverseString(String s) {
        if(s == null || s.length() < 2)
            return s;
        return reverseString(s.substring(1)) + s.charAt(0);
    }
```

普通解法

```java
public String reverseString(String s) {
  	char[] c = s.toCharArray();
  	int i = 0;
  	int j = s.length() - 1;
  	char tmp;
  	while(i < j){
      	tmp = c[i];
      	c[i] = c[j];
      	c[j] = tmp;
      	i++;
      	j--;
  	}
  	return new String(c);
}
```
## 415. Add Strings
Given two non-negative numbers `num1` and `num2` represented as string, return the sum of `num1` and `num2`.

**Note:**

1. The length of both `num1` and `num2` is < 5100.
2. Both `num1` and `num2` contains only digits `0-9`.
3. Both `num1` and `num2` does not contain any leading zero.
4. You **must not use any built-in BigInteger library** or **convert the inputs to integer** directly.

solution:



```java
public String addStrings(String num1, String num2) {
    char[] n1 = num1.toCharArray();
    char[] n2 = num2.toCharArray();
    int i = n1.length - 1;
    int j = n2.length - 1;
    StringBuilder sb = new StringBuilder();
    int sum = 0, carry = 0;
    while(i>=0 || j >=0){
        int first =  i >= 0 ? n1[i] - '0' : 0;
        int second = j >= 0 ? n2[j] - '0' : 0;
        sum = first + second + carry;
        if(sum < 10){   //如果没有进位
            sb.insert(0,sum);
            carry = 0;
            sum = 0;
        }
        if(sum >= 10){  //进位
            sb.insert(0,sum-10); //在首位置 插入数字
            carry = 1;  //设置进位
            sum = 0;
        }
        i--;
        j--;
    }
    if(carry == 1)  //如果最后还有进位 ，则在首位加1
        sb.insert(0,"1");
    return sb.toString();
}
```
leetcode 简洁的方法

```java
public String addStrings(String num1, String num2) {
        StringBuilder sb = new StringBuilder();
        int carry = 0;
        for(int i = num1.length() - 1, j = num2.length() - 1; i >= 0 || j >= 0; i--, j--){
            int x = i < 0 ? 0 : num1.charAt(i) - '0';
            int y = j < 0 ? 0 : num2.charAt(j) - '0';
            sb.append((x + y + carry) % 10);
            carry = (x + y + carry) / 10;
        }
        if(carry != 0)
            sb.append(carry);
        return sb.reverse().toString();
    }
```