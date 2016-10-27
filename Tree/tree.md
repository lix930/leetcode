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

## 404. Sum of Left Leaves
Find the sum of all left leaves in a given binary tree.

**Example:**

```
    3
   / \
  9  20
    /  \
   15   7

There are two left leaves in the binary tree, with values 9 and 15 respectively. Return 24.
```
solution：
要熟练使用递归
```java
public int sumOfLeftLeaves(TreeNode root) {
    if(root == null)
      return 0;
    int sum = 0;
    if(root.left != null){ //如果左子树不为空
      if(root.left.right == null && root.left.left == null){ //这个节点为叶子节点
        sum += root.left.val;
      }else{
        sum += sumOfLeftLeaves(root.left);//递归处理左子树
      }
    }
    if(root.right != null){
      sum += sumOfLeftLeaves(root.right);//递归处理右子树
    }
    return sum;
}
```

## 144. Binary Tree Preorder Traversal
Given a binary tree, return the *preorder* traversal of its nodes' values.

For example:
Given binary tree `{1,#,2,3}`,

```
   1
    \
     2
    /
   3

```

return `[1,2,3]`.

solution: 递归方法

```java
public List<Integer> preorderTraversal(TreeNode root) {
    List<Integer> list = new ArrayList<Integer>();
    if(root != null){
        list.add(root.val);
        list.addAll(preorderTraversal(root.left));
        list.addAll(preorderTraversal(root.right));
    }
    return list;
}
```
遍历方法：

```java
public List<Integer> preorderTraversal(TreeNode root) { //中序遍历
    List<Integer> list = new ArrayList<Integer>();
    Stack<TreeNode> stack = new Stack<TreeNode>();
    if(root != null){
        stack.push(root);
        while(!stack.isEmpty()){
            TreeNode node = stack.pop();
            list.add(node.val);     //处理结点
            if(node.right != null)  // 把右子树加入栈
                stack.push(node.right);
            if(node.left != null)  
                stack.push(node.left);
        }
    }
    return list;
}
```

## 94. Binary Tree Inorder Traversal


Given a binary tree, return the *inorder* traversal of its nodes' values.

For example:
Given binary tree `[1,null,2,3]`,

```
   1
    \
     2
    /
   3

```

return `[1,3,2]`.

solution：

递归：



```java
public List<Integer> inorderTraversal(TreeNode root) {
    List<Integer> list = new ArrayList<Integer>();
    helper(list, root);
    return list;
}

public void helper(List<Integer> list, TreeNode root){
    if(root != null){
        helper(list,root.left);
      	list.add(root.val);
        helper(list,root.right); 
    }
}
```
遍历：

```java
public List<Integer> inorderTraversal(TreeNode root) {
    List<Integer> list = new ArrayList<Integer>();
    Stack<TreeNode> stack = new Stack<TreeNode>();
    TreeNode node = root;
    while(node != null || !stack.isEmpty()){
      while(node != null){
        stack.push(node);
        node = node.left;
      }
      if(!stack.isEmpty()){
        node = stack.pop();
        list.add(node.val);
        node = node.right;
      }
    }
    return list;
}
```

##　145. Binary Tree Postorder Traversal
Given a binary tree, return the *postorder* traversal of its nodes' values.

For example:
Given binary tree `{1,#,2,3}`,

```
   1
    \
     2
    /
   3

```

return `[3,2,1]`.

solution：递归



```java
public List<Integer> postorderTraversal(TreeNode root) {
    List<Integer> list = new ArrayList<Integer>();
    helper(list, root);
    return list;
}

public void helper(List<Integer> list, TreeNode root){  //辅助函数，用于输出list数据
    if(root != null){
        helper(list,root.left);
        helper(list,root.right);
        list.add(root.val);   //后序遍历
    }
}
```
遍历：



```java
public List<Integer> postorderTraversal(TreeNode root) {
    List<Integer> list = new ArrayList<Integer>();
    Stack<TreeNode> stack = new Stack<TreeNode>();
    TreeNode node = root;
    TreeNode pre = null; //pre表示最近出栈的节点，用于判断是否
                         //是node节点的右孩子，如果是的话，
                         //就可以访问node结点
    while(node != null || !stack.isEmpty()){
        while(node != null ){   //将栈顶结点的左孩子相继入栈
            stack.push(node);
            node = node.left;
        }
        if(!stack.isEmpty()){
            node = stack.peek();
            if(node.right != null && node.right != pre){  //
                node = node.right;
            }else{
                node = stack.pop();
                list.add(node.val);
                pre = node;
                node = null;
            }
        }  
    }
    return list;
}
```