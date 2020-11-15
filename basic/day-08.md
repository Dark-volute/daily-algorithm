[https://leetcode-cn.com/problems/rotate-list/](https://leetcode-cn.com/problems/rotate-list/)

## 思路

1. 获取单链表的倒数第N + 1 与倒数第N个节点
2. 将倒数第N + 1个节点的next指向null
3. 将链表尾节点的next指向head
4. 返回倒数第N个节点

```js
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} head
 * @param {number} k
 * @return {ListNode}
 */
var rotateRight = function(head, k) {
    if(!head || !head.next) return head
    let count = 0, now = head
    while(now){
        now = now.next
        count++
    }
    k = k % count
    let fast = head, slow = head;
    while (fast.next) {
        if (k-- <= 0) {
            slow = slow.next
        }
        fast = fast.next
    }
    fast.next = head
    let res = slow.next
    slow.next = null
    return res
};
```

## 复杂度分析

时间复杂度：$O(N)$
空间复杂度：$O(1)$
