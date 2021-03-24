[https://leetcode-cn.com/problems/same-tree](https://leetcode-cn.com/problems/same-tree)

## 思路
比较两棵树的结构，可以对两棵树同时进行层级遍历，在遍历中比较节点，如果有不同的节点就提前退出。

需要注意的是遍历过程中空节点也要入列。

## 代码
JavaScript Code

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} p
 * @param {TreeNode} q
 * @return {boolean}
 */
var isSameTree = function (p, q) {
    const queueP = [p];
    const queueQ = [q];

    while (queueP.length && queueQ.length) {
        let lenP = queueP.length;
        let lenQ = queueQ.length;

        // 如果两棵树同一层的节点数都不同，肯定不是同一棵树
        if (lenP !== lenQ) return false;

        while (lenP-- && lenQ--) {
            const nodeP = queueP.shift();
            const nodeQ = queueQ.shift();

            // 两个节点都是 null, 直接继续比较下一个节点
            if (!nodeP && !nodeQ) continue;
            // 遇到不同的节点，说明不是同一棵树，提前返回
            if (!nodeP || !nodeQ || nodeP.val !== nodeQ.val) return false;

            // 将下一层的节点入列，空节点也要入列
            queueP.push(nodeP.left, nodeP.right);
            queueQ.push(nodeQ.left, nodeQ.right);
        }
    }
    return true;
};
```

## 复杂度分析
时间复杂度：$O(N)$，N 为二叉树的节点数。
空间复杂度：$O(logN)$，N 为二叉树的节点数。