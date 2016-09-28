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
