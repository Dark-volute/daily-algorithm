[https://leetcode-cn.com/problems/maximum-depth-of-binary-tree](https://leetcode-cn.com/problems/maximum-depth-of-binary-tree)

## 思路
递归地分别计算出左子树和右子树的高度，取最大值加一，就是当前二叉树的最大深度。

假设我们已经计算出了左子树的最大深度是 1，右子树的最大深度是 2，那整棵二叉树的的最大深度就是左右子树最大深度的最大值加上根节点，也就是 3。

接下来我们只需要递归地去计算左右子树的高度：

base condition: 首先在递归中很重要的事情就是找到递归的出口，在这道题目中，明显能想到的出口是：

当遍历到叶子节点的时候：if not root.left and not root.right，这时候我们需要 return 1。
还有一种情况是，当前遍历的节点为 null，这时候我们只需要 return 0 就好了。
如果当前节点有左子树，需要递归计算左子树的高度 leftHeight = maxDepth(root.left)。

如果当前节点有右子树，需要递归计算右子树的高度 rightHeight = maxDepth(root.right)。

取左右子树最大高度的最大值，加上当前节点返回 max(leftHeight, rightHeight) + 1 即可。

## 代码
```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number}
 */
var maxDepth = function (root) {
    if (!root) return 0;
    if (!root.left && !root.right) return 1;
    return Math.max(maxDepth(root.left), maxDepth(root.right)) + 1;
}
```

## 复杂度分析
时间复杂度：$O(N)$，N 为二叉树的节点数，因为每个节点都只遍历一次。
空间复杂度：$O(N)$，递归栈的空间。