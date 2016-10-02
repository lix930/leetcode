## 137. Delete Node in a Linked List

Write a function to delete a node (except the tail) in a singly linked list, given only access to that node.

Supposed the linked list is `1 -> 2 -> 3 -> 4` and you are given the third node with value `3`, the linked list should become `1 -> 2 -> 4` after calling your function.

solution: 这题没有提供头结点，只是删除node，可以先把node的后一个节点复制到node，然后删除node的后一个节点。

```java
/**
*  Definition for singly-linked list.
*  public class ListNode {
*  int val;
*  ListNode next;
*  ListNode(int x) { val = x; }
*  }
    */
   public class Solution {
    public void deleteNode(ListNode node) {
        node.val = node.next.val;
        node.next = node.next.next;
    }
   }
```



## 206. Reverse Linked List
Reverse a singly linked list.

solution : 
递归:
递归反转法：在反转当前节点之前先反转后续节点。这样从头结点开始，层层深入直到尾结点才开始反转指针域的指向。简单的说就是从尾结点开始，逆向反转各个结点的指针域指向.
   **head**：是前一结点的指针域（PS：前一结点的指针域指向当前结点）
   **head.next**：是当前结点的指针域（PS：当前结点的指针域指向下一结点）
   **newHead**：是反转后新链表的头结点（即原来单链表的尾结点）
```java
/**

*  Definition for singly-linked list.
*  public class ListNode {
*  int val;
*  ListNode next;
*  ListNode(int x) { val = x; }
*  }
    */
public class Solution {
    public ListNode reverseList(ListNode head) {
        if(head == null || head.next == null)
            return head;
        ListNode newHead = reverseList(head.next);
        head.next.next = head; //使后结点指向头结点
        head.next = null;      //删除头结点指向后结点的关系
        return newHead;
    }
}
```

遍历：

**遍历反转法：**递归反转法是从后往前逆序反转指针域的指向，而遍历反转法是从前往后反转各个结点的指针域的指向。

   **基本思路**是：将当前节点cur的下一个节点 cur.next缓存到temp后，然后更改当前节点指针指向上一结点pre。也就是说在反转当前结点指针指向前，先把当前结点的指针域用tmp临时保存，以便下一次使用，其过程可表示如下：
**pre**		上一结点
**cur **		 当前结点
**tmp ** 	 临时结点，用于保存当前结点的指针域（即下一结点）

```java
public class Solution {
    public ListNode reverseList(ListNode head) {
        if(head == null || head.next == null)
            return head;
        ListNode cur = head.next;
        ListNode pre = head;
        ListNode tmp = null;
        while(cur != null){
            //保存cur的下一个结点
            tmp = cur.next;
            //反转指针
            cur.next = pre;
            // 推进
            pre = cur;
            cur = tmp;
        }
        //清除head.next的指向
        head.next = null;
        //返回新的头指针
        return pre;
    }
}
```
## 21. Merge Two Sorted Lists
Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

solution: 

递归方法： 也就是归并排序的合并部分。

```java
public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
    if(l1 == null)
        return l2;
    if(l2 == null)
        return l1;
    if( l1.val < l2.val){
        l1.next = mergeTwoLists(l1.next, l2);
        return l1;
    }else{
        l2.next = mergeTwoLists(l1, l2.next);
        return l2;
    }
}
```
遍历方法：新建一个表头，然后遍历两个链表，把最小的取出来。

```java
public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
    if(l1 == null && l2 == null)
        return null;
    if(l1 == null)
        return l2;
    if(l2 == null)
        return l1;
    ListNode newHead = new ListNode(0);
    ListNode cur = newHead;
    while(l1 != null && l2 != null){
        if(l1.val <= l2.val){
            cur.next = l1;
            l1 = l1.next;
        }else{
            cur.next = l2;
            l2 = l2.next;
        }
        cur = cur.next;
    }
    if (l1 == null)
        cur.next = l2;
    if (l2 == null)
        cur.next = l1;
    return newHead.next;
}
```
## 83. Remove Duplicates from Sorted List
Given a sorted linked list, delete all duplicates such that each element appear only once.

For example,
Given `1->1->2`, return `1->2`.
Given `1->1->2->3->3`, return `1->2->3`.
solution: 遍历链表如果当前节点与next节点值相同，则cur.next = cur.next.next, 否则 cur = cur.next;
```java
public ListNode deleteDuplicates(ListNode head) {
        ListNode cur = head;
        while(cur != null){
            if (cur.next == null)
                break;
            if(cur.val == cur.next.val){
                cur.next = cur.next.next;
            }else{
                cur = cur.next;
            }
        }
        return head;
    }
```
## 24. Swap Nodes in Pairs
Given a linked list, swap every two adjacent nodes and return its head.

For example,
Given `1->2->3->4`, you should return the list as `2->1->4->3`.

Your algorithm should use only constant space. You may **not** modify the values in the list, only nodes itself can be changed.
solution:
```java
public ListNode swapPairs(ListNode head) {
    
    if (head == null) {
        return null;
    }
    ListNode newhead = new ListNode(-1);//dummy
    newhead.next = head;
    ListNode temp = newhead;
    
    ListNode one = null;
    ListNode two = null;
    
    // {dummy->1->2->3->4->null}
    //explanation for one loop rest are same.
    
    
    while(temp.next!= null && temp.next.next!=null) {
        // temp points to dummy in the beginning.
        // one -> 1
        one = temp.next;
        //two -> 2
        two = temp.next.next;
        // 1-> = 2.next = 3;
        one.next=two.next;
        // 2-> = 1
        two.next = one;
        //now dummy should point to 2
        //if the below is not done dummy->1;
        temp.next = two;
        // temp was pointing to dummy
        //temp->1
        temp = one;
        // now { dummy->2->1->3->4 }
    }
    return newhead.next;
```

## 141. Linked List Cycle
Given a linked list, determine if it has a cycle in it.

Follow up:
Can you solve it without using extra space?

solution: 设置两个指针 slow, fast, slow每次走一步，fast每次走两步。
如果某个时刻 slow==fast 则说明 链表有环
```java
public boolean hasCycle(ListNode head) {
        ListNode slow = head;
        ListNode fast = head;
        if (head == null)
            return false;
        while(fast != null && fast.next != null){
            slow = slow.next;
            fast = fast.next.next;
            if(slow == fast)
                return true;
        }
        return false;
    }
```


## 19. Remove Nth Node From End of List
Given a linked list, remove the nth node from the end of list and return its head.

For example,
```
   Given linked list: 1->2->3->4->5, and n = 2.

   After removing the second node from the end, the linked list becomes 1->2->3->5.
```
**Note**:
Given n will always be valid.
Try to do this in one pass.

solution: 这是一个快慢指针路程的问题，设置一个slowNode, fastNode,用fastNode遍历链表,每次遍历fastNode后移一位，n--,当n<=0时 slowNode后移一位。
slowNode找到倒数第n个结点后，进行删除操作。

```java
public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode newHead = new ListNode(-1);
        newHead.next = head;
        ListNode slowNode = newHead;
        ListNode fastNode = newHead;
        while(fastNode.next != null){
            if(n <= 0)
                slowNode = slowNode.next;
            fastNode = fastNode.next;
            n--;
        }
        if(slowNode.next != null)
            slowNode.next = slowNode.next.next;
        return newHead.next;
    }
```
## 160. Intersection of Two Linked Lists

Write a program to find the node at which the intersection of two singly linked lists begins.

For example, the following two linked lists:

```
A:          a1 → a2
                   ↘
                     c1 → c2 → c3
                   ↗            
B:     b1 → b2 → b3

```

begin to intersect at node c1.

**Notes:**

- If the two linked lists have no intersection at all, return `null`.
- The linked lists must retain their original structure after the function returns.
- You may assume there are no cycles anywhere in the entire linked structure.
- Your code should preferably run in O(n) time and use only O(1) memory.

**solution**: 可以记录两个链表的长度，用lenA-lenB（即 6-5 = 1） 得到交点前的offset，将长的链表置于offset处（即b2处），然后p1,p2一起后移，直到p1==p2, 返回交点p1（即c1）,如果没有交点 则返回null.



```java
public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
    if(headA == null || headB == null) //边界条件
        return null;
    //计算长度
    int lenA = length(headA);
    int lenB = length(headB);
    //偏置
    while(lenA > lenB){
        headA = headA.next;
        lenA--;
    }
    while(lenA < lenB){
        headB = headB.next;
        lenB--;
    }
    // 找出交点 如果没交点 headA 为null
    while(headA != headB){
        headA = headA.next;
        headB = headB.next;
    }
    return headA;
    
}

private int length(ListNode head){
    int length = 0;
    while(head != null){
        head = head.next;
        length++;
    }
    return length;
}
```