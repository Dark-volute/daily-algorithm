[https://leetcode-cn.com/problems/n-queens-ii/](https://leetcode-cn.com/problems/n-queens-ii/)

## 思路

通过三个集合columns, diagonals1, diagonals2， 记录每次深度优先遍历摆放皇后的位置，合理剪枝。

## 代码
```js
var totalNQueens = function (n) {
  const columns = new Set();
  const diagonals1 = new Set();
  const diagonals2 = new Set();
  let count = 0
  const defs = (row, columns, diagonals1, diagonals2) => {
    if (row === n ) {
        count++
        return
    }
    for (let i = 0; i < n; i++) {
      if (columns.has(i)) {
        continue;
      }
      const diagonal1 = row - i;
      if (diagonals1.has(diagonal1)) {
        continue;
      }
      const diagonal2 = row + i;
      if (diagonals2.has(diagonal2)) {
        continue;
      }
      columns.add(i);
      diagonals1.add(diagonal1);
      diagonals2.add(diagonal2);
      defs(row + 1, columns, diagonals1, diagonals2);
      columns.delete(i);
      diagonals1.delete(diagonal1);
      diagonals2.delete(diagonal2);
    }
  }
  defs(0, columns, diagonals1, diagonals2);
  return count
}

```

### 复杂度
时间复杂度：$O(n!)$
空间复杂度：$O(n)$