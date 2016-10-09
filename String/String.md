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