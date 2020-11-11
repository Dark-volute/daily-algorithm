## 思路
- 遍历整个链表,同时将每个节点都插入哈希表,
- 如果当前节点在哈希表中不存在,继续遍历,
- 如果存在,那么当前节点就是环的入口节点

```js
let data = new Set();
while (head) {
  if (data.has(head)) {
    return head;
  } else {
    data.add(head);
  }
  head = head.next;
}
return null;
```

## 复杂度分析

时间复杂度：$O(N)$
空间复杂度：$O(N)$
