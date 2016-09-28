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