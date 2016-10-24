## 104. Maximum Depth of Binary Tree
Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

solution：用递归来做
```java
public int maxDepth(TreeNode root) {
    if(root == null)
    	return 0;
  	else{
    	return 1 + Math.max(maxDepth(root.left), maxDepth(root.right));
  }
}
```


## 226. Invert Binary Tree

Invert a binary tree.

```
     4
   /   \
  2     7
 / \   / \
1   3 6   9
```

to

```
     4
   /   \
  7     2
 / \   / \
9   6 3   1
```

solution：递归
```java
public TreeNode invertTree(TreeNode root) {
        if(root == null)
            return null;
        
        final TreeNode left = root.left;
        final TreeNode right = root.right;
        root.left = invertTree(right);
        root.right = invertTree(left);
        return root;
    }
```
非递归版本

```java
public TreeNode invertTree(TreeNode root) {
   
        if (root == null) {
            return null;
        }
        final Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
		//使用一个辅助队列
        while(!queue.isEmpty()) {
            final TreeNode node = queue.poll();
            final TreeNode left = node.left;
            node.left = node.right;
            node.right = left;

            if(node.left != null) {
                queue.offer(node.left);
            }
            if(node.right != null) {
                queue.offer(node.right);
            }
        }
        return root;
    }
```



## 100. Same Tree
Given two binary trees, write a function to check if they are equal or not.

Two binary trees are considered equal if they are structurally identical and the nodes have the same value.

solution： 很基本的题目

```java
public boolean isSameTree(TreeNode p, TreeNode q) {
    if(p == null && q == null)
        return true;
    else if(p != null && q != null){
        if(p.val == q.val)
            if(isSameTree(p.left, q.left) && isSameTree(p.right, q.right))
                return true;
    }
    return false;
}
```