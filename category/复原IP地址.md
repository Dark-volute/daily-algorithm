[https://leetcode-cn.com/problems/restore-ip-addresses/](https://leetcode-cn.com/problems/restore-ip-addresses/)

## 思路

- 以 "25525511135" 为例，做第一步时我们有几种选择？

  1. 选 "2" 作为第一个片段
  2. 选 "25" 作为第一个片段
  3. 选 "255" 作为第一个片段
- 能切三种不同的长度，切第二个片段时，又面临三种选择。
- 这会向下分支形成一棵树，我们用 DFS 去遍历所有选择，必要时提前回溯。
- 约束条件限制了当前的选项，这道题的约束条件是：
  1. 一个片段的长度是 1~3
  2. 片段的值范围是 0~255
  3. 不能是 "0x"、"0xx"



## 代码
```js

var restoreIpAddresses = function(s) {
  let res = []
  const dfs = (path, start) => {
      if (path.length === 4 && start === s.length) {
          res.push(path.join('.'))
          return
      }
      if (path.length === 4 && start < s.length) {
          return
      }
      for (let i = 1; i <= 3; i++) {
          if (start + i > s.length) return               // 加上要切的长度就越界
          const str = s.substring(start, start + i)   
          if (i !== 1 && s[start] === '0') return;     // 不能切出'0x'、'0xx'
          if (i === 3 && +str > 255) return;           // 不能超过255
          path.push(str)
          dfs(path, i + start)
          path.pop()
      }
  }
  dfs([], 0)
  return res
};

```

## 复杂度

时间复杂度 $O(3 ^ 4 * ∣s∣)$
空间复杂度 $0(4)$
