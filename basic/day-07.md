[https://leetcode-cn.com/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof/]
## 思路
快慢指针，快指针结束时，慢指针正好位倒数k项

```js
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} head
 * @param {number} k
 * @return {ListNode}
 */
var getKthFromEnd = function(head, k) {
    let fast = head, slow = head;
    while (fast.next) {
        if (k-- <= 1) {
            slow = slow.next
        }
        fast = fast.next
    }
    return slow
};
```

## 复杂度分析

时间复杂度：$O(N)$
空间复杂度：$O(1)$
