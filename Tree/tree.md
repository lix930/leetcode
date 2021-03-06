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
        Queue<TreeNode> queue = new LinkedList<TreeNode>();
        if(root!= null){
            queue.offer(root);
            while(!queue.isEmpty()){   //使用层序遍历 
                TreeNode node = queue.poll();
                if(node.left != null){
                    queue.offer(node.left);
                }
                if(node.right != null){
                    queue.offer(node.right);
                }
                TreeNode tmp = node.left;   //交换左右子树
                node.left = node.right;
                node.right = tmp;
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

## 111. Minimum Depth of Binary Tree
Given a binary tree, find its minimum depth.

The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.

solution: 

```java
public int minDepth(TreeNode root) {
    if(root == null)
        return 0;
    if(root.left == null || root.right == null)  //处理但结点只有一个孩子的情况
        return Math.max(minDepth(root.left), minDepth(root.right)) + 1;
    return Math.min(minDepth(root.left), minDepth(root.right)) + 1;
}
```
## 110. Balanced Binary Tree

Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of *every* node never differ by more than 1.

solution：该算法需要O(N)的时间，O(H)的空间， H为树的高度。

```java
public class Solution {
    public boolean isBalanced(TreeNode root) {
        if(root == null)
            return true;
        if(checkHeight(root) == -1)
            return false;
        else
            return true;
    }
    
    public int checkHeight(TreeNode root) {
        if(root == null)
            return 0;
        int leftHight = checkHeight(root.left); //检查左子树是否平衡
        if(leftHight == -1)
            return -1;
        int rightHight = checkHeight(root.right);//检查右子树是否平衡
        if(rightHight == -1)
            return -1;
        int diff = leftHight - rightHight;
        if(Math.abs(diff) > 1) //检查当前结点是否平衡
            return -1; //不平衡
        else//返回高度
            return Math.max(checkHeight(root.left), checkHeight(root.right)) + 1;
    }
}
```
## 101. Symmetric Tree

Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

For example, this binary tree `[1,2,2,3,4,4,3]` is symmetric:

```
    1
   / \
  2   2
 / \ / \
3  4 4  3

```

But the following `[1,2,2,null,3,null,3]` is not:

```
    1
   / \
  2   2
   \   \
   3    3
```

solution: 即判断左右子树是否为镜像（反转）

递归方法：

```java
public boolean isSymmetric(TreeNode root) {
    if(root==null) return true;
    return isMirror(root.left,root.right);
}
public boolean isMirror(TreeNode p, TreeNode q) {
    if(p==null && q==null) return true;
    if(p==null || q==null) return false;
    return (p.val==q.val) && isMirror(p.left,q.right) && isMirror(p.right,q.left);
}
```
##  102. Binary Tree Level Order Traversal

Given a binary tree, return the *level order* traversal of its nodes' values. (ie, from left to right, level by level).

For example:
Given binary tree `[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7

```

return its level order traversal as:

```
[
  [3],
  [9,20],
  [15,7]
]
```
solution：主要是考虑输出的格式，
```java
public List<List<Integer>> levelOrder(TreeNode root) {
    List<List<Integer>> result = new ArrayList<>();
    Queue<TreeNode> queue = new LinkedList<>();  
    if(root == null)
        return result;
    queue.offer(root);
    while(!queue.isEmpty()){
        int nodeNum = queue.size(); //记录当前层 结点的个数
        List<Integer> subList= new ArrayList<>();
        for(int i = 0; i < nodeNum; i++){
            TreeNode node = queue.poll();
            if(node.left != null)
                queue.offer(node.left);
            if(node.right != null)
                queue.offer(node.right);
            subList.add(node.val);    
        }
        result.add(subList);
    }
    return result;
}
```
## 107. Binary Tree Level Order Traversal II

Given a binary tree, return the *bottom-up level order* traversal of its nodes' values. (ie, from left to right, level by level from leaf to root).

For example:
Given binary tree `[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7

```

return its bottom-up level order traversal as:

```
[
  [15,7],
  [9,20],
  [3]
]
```
solution : 跟上一题一样，注意List的插入位置就行了
```java
public List<List<Integer>> levelOrderBottom(TreeNode root) {
        List<List<Integer>> result = new LinkedList<List<Integer>>();
        if(root == null)
            return result;
        Queue<TreeNode> queue = new LinkedList<TreeNode>();
        queue.offer(root);
        while(!queue.isEmpty()){
            List<Integer> subList = new LinkedList<Integer>();
            int nodeNum = queue.size();
            for(int i = 0; i < nodeNum; i++){
                TreeNode node = queue.poll();
                if(node.left != null)
                    queue.offer(node.left);
                if(node.right != null)
                    queue.offer(node.right);
                subList.add(node.val);
            }
            result.add(0,subList);  //在首位置插入子List
        }
        return result;
    }
```

## 112. Path Sum

Given a binary tree and a sum, determine if the tree has a root-to-leaf path such that adding up all the values along the path equals the given sum.

For example:

Given the below binary tree and 

```
sum = 22
```

,

```
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \      \
        7    2      1

```

return true, as there exist a root-to-leaf path `5->4->11->2` which sum is 22.
solution:

本题所需要做的是找到一条从根节点到叶子节点的路径，因此我们需要去枚举每一条路径的和，看其值是否等于目标值。

直接才用遍历的方法，用一个参数表示从根节点到当前节点的权值之和。

当遍历到一个节点时：

- 若该节点为空：返回False。
- 若该节点为叶子节点：判断当前权值和是否等于目标值。
- 若该节点不为叶子节点：递归处理其左右子树。

递归处理整个二叉树，就能够判定出结果。

```java
public boolean hasPathSum(TreeNode root, int sum) {
        if(root == null)
            return false;
        if(root.left == null && root.right == null && sum - root.val == 0)
            return true;
        return hasPathSum(root.left, sum - root.val) || hasPathSum(root.right, sum - root.val);
    }
```