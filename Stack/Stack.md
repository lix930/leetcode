

## 132. Implement Queue using Stacks


Implement the following operations of a queue using stacks.

- push(x) -- Push element x to the back of queue.
- pop() -- Removes the element from in front of queue.
- peek() -- Get the front element.
- empty() -- Return whether the queue is empty.

Notes:

- You must use *only* standard operations of a stack -- which means only `push to top`, `peek/pop from top`, `size`, and `is empty` operations are valid.
- Depending on your language, stack may not be supported natively. You may simulate a stack by using a list or deque (double-ended queue), as long as you use only standard operations of a stack.
- You may assume that all operations are valid (for example, no pop or peek operations will be called on an empty queue).

solution:


​    

```java
class MyQueue {
    Stack<Integer> stack1 = new Stack<>();
    Stack<Integer> stack2 = new Stack<>();
  
    public void push(int x) {
        stack1.push(x);
    }
  
    public void pop() {
		//如果栈2为空，则把栈1 pop 到栈2中
        if(stack2.isEmpty()){
            while(!stack1.isEmpty()){
                stack2.push(stack1.pop());
            }
        }
        stack2.pop();
    }

    public int peek() {
        if(stack2.isEmpty()){
            while(!stack1.isEmpty()){
                stack2.push(stack1.pop());
            }
        }
        return stack2.peek();
        }

    public boolean empty() {
        return (stack1.size() + stack2.size()) == 0;
    }
}
```


## 225. Implement Stack using Queues
Implement the following operations of a stack using queues.

- push(x) -- Push element x onto stack.
- pop() -- Removes the element on top of the stack.
- top() -- Get the top element.
- empty() -- Return whether the stack is empty.

Notes:

- You must use *only* standard operations of a queue -- which means only `push to back`, `peek/pop from front`, `size`, and `is empty` operations are valid.
- Depending on your language, queue may not be supported natively. You may simulate a queue by using a list or deque (double-ended queue), as long as you use only standard operations of a queue.
- You may assume that all operations are valid (for example, no pop or top operations will be called on an empty stack).

solution: 使用两个queue,

- push(x) 时 

  ​	size==0时，任选一个队列

  ​	size!=0时，选择一个不为空的队列

- pop() 与 top() 

  ​	两个队列来回倒腾 

  ​	最后一个元素特殊处理(把前面的元素都移动到另一个queue,在执行pop或top)



```java
class MyStack {
    Queue<Integer> queue1 = new LinkedList<Integer>();
    Queue<Integer> queue2 = new LinkedList<Integer>();

    public void push(int x) {
        if(!queue1.isEmpty())
            queue1.offer(x);
        else
            queue2.offer(x);
    }
	//主要是来回倒腾
    public void pop() {
        if(!queue1.isEmpty()){
           while(queue1.size()>1){
               queue2.offer(queue1.poll());
           } 
           queue1.poll();
        }else{
            while(queue2.size()>1){ //队尾前 的元素都移到另一个队列
               queue1.offer(queue2.poll());
           } 
           queue2.poll();
        }
    }

    public int top() {
        if(!queue1.isEmpty()){
           while(queue1.size()>1){
               queue2.offer(queue1.poll());
           } 
           int k = queue1.poll(); //记录值
           queue2.offer(k); //移动到另一个队列
           return k;
        }else{
            while(queue2.size()>1){
               queue1.offer(queue2.poll());
           } 
           int k = queue2.poll();
           queue1.offer(k);
           return k;
        }
    }

    public boolean empty() {
        return queue1.isEmpty() && queue2.isEmpty();
    }
}
```
## 155. Min Stack

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

- push(x) -- Push element x onto stack.
- pop() -- Removes the element on top of the stack.
- top() -- Get the top element.
- getMin() -- Retrieve the minimum element in the stack.

**Example:**

```
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> Returns -3.
minStack.pop();
minStack.top();      --> Returns 0.
minStack.getMin();   --> Returns -2.
```
solution: 

1. 使用两个栈，一个栈存储最小值。



```java
public class MinStack {
    Stack<Integer> stack = new Stack<Integer>();
    Stack<Integer> minStack = new Stack<Integer>();
    public MinStack() {

    }

    public void push(int x) {
        if(minStack.isEmpty()){ //minStack为空时，push到两个栈
            stack.push(x);
            minStack.push(x);
        }else{ //minStack不为空时，minStack入栈（x与min）中较小的值。
            stack.push(x);
            int min = minStack.peek();
            minStack.push(Math.min(min, x));
        }
    }

    public void pop() {
        stack.pop();
        minStack.pop();
    }

    public int top() {
        return stack.peek();
    }

    public int getMin() {
        return minStack.peek();
    }
}
```



##  判断入栈，出栈序列是否正确

```java
public boolean checkValid(Integer[] pushSequence, Integer[] popSequence) {
	Stack<Integer> stack = new Stack<Integer>();	
	int i = 0; // push pointer
	for (Integer k : popSequence) { // 遍历弹栈序列
		if (!stack.isEmpty() && stack.peek().equals(k)) { 
            // 如果当前元素和栈顶元素相等，则stack.pop();
			stack.pop();
		} else {
			while (true) {
				//如果 指针越界，则说明弹栈序列不合法，返回false
				if (i >= pushSequence.length) {
					return false;
				}
				//依次压栈 ，直到两个序列的 当前元素相等
				if (pushSequence[i].equals(k)) {
					i++;
					break;
				} else {
					stack.push(pushSequence[i]);
					i++;
				}
			}
		}
	}
	//最终如果没有返回false，说明弹栈序列正确。
	return true;
}
```


## 20. Valid Parentheses
Given a string containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

The brackets must close in the correct order, `"()"` and `"()[]{}"` are all valid but `"(]"` and `"([)]"` are not.        

solution: 遇到左括号进栈， 遇到右括号，如果不会空则出栈，对比匹配情况

```java
public boolean isValid(String s) {
    Stack<Character> stack = new Stack<Character>();
    for(char x : s.toCharArray()){
        if(x == '(') stack.push(')');
        if(x == '[') stack.push(']');
        if(x == '{') stack.push('}');
        
        if(x == ')' || x == ']' || x == '}'){
            if(stack.isEmpty())  // 栈为空 返回false
                return false;
            if(x == stack.peek()) //如果匹配 则弹栈
                stack.pop();
            else 
                return false; //不匹配 返回false
        }
    }
    if(stack.isEmpty()) //栈为空 说明全都匹配
        return true;
    else
        return false; 
}
```



## 71. Simplify Path
Given an absolute path for a file (Unix-style), simplify it.

For example,
**path** = `"/home/"`, => `"/home"`
**path** = `"/a/./b/../../c/"`, => `"/c"`

**Corner Cases:**Did you consider the case where **path** = `"/../"`?
In this case, you should return `"/"`.Another corner case is the path might contain multiple slashes `'/'` together, such as `"/home//foo/"`.
In this case, you should ignore redundant slashes and return `"/home/foo"`.

solution： 将路径以"/"分开，跳过".", "//",""，如果为".."则弹栈，其余的压栈。

最后将栈逆序，并按路径格式输出。

```java
public String simplifyPath(String path) {
    LinkedList<String> stack = new LinkedList<String>();
    String[] str = path.split("/");
    for(String x : str){
        if(".".equals(x) || "".equals(x))
            continue;
        if("..".equals(x)){
            if(!stack.isEmpty())
                stack.pop();
        }
        else
            stack.push(x);    
    }
    if(stack.isEmpty())
        return "/";
    else{
        Collections.reverse(stack);
        StringBuilder sb = new StringBuilder();
        while(!stack.isEmpty()){
            sb.append("/").append(stack.pop());
        }
        return sb.toString();
    }
    
}
```