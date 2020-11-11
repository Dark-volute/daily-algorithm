
[https://leetcode-cn.com/problems/swap-nodes-in-pairs/](https://leetcode-cn.com/problems/swap-nodes-in-pairs/)

### 思路


### 代码
```js
/**
 * @param {ListNode} head
 * @return {ListNode}
 */
var swapPairs = function (head) {
    const dummy = new ListNode(null, head);
    let prev = dummy;
    let cur = prev.next;

    while (cur && cur.next) {
        const next = cur.next;
        cur.next = next.next;
        next.next = cur;
        prev.next = next;

        prev = cur;
        cur = cur.next;
    }
    return dummy.next;
};
```

