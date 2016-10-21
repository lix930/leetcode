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


