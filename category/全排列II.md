[https://leetcode-cn.com/problems/permutations-ii/](https://leetcode-cn.com/problems/permutations-ii/)

## 思路

比如[1,1,2]，先选第一个1，和先选第二个1，往后的情况是一样的。
即，“同一层” 的选项出现重复，或者说，当前可选的选项出现重复。

重复的选项要修剪掉，为了方便在迭代中识别出重复，先对 nums 中数字升序排序，使得相同的数字相邻。

充分地剪枝
对应上面第一点，我们使用一个 used 数组记录使用过的数字，使用过了就不再使用：

if (used[i]) {
    continue;
}
对应上面第二点，如果当前的选项nums[i]，与同一层的前一个选项nums[i-1]相同，且nums[i-1]存在，且没有被使用过，则忽略选项nums[i]。
如果nums[i-1]被使用过，它会被第一条修剪掉，不是选项了，即便它和nums[i]重复，nums[i]还是可以选的。

if (nums[i - 1] == nums[i] && i - 1 >= 0 && !used[i - 1]) {
    continue;
}
比如[1,1,2]，第一次选了第一个1，第二次是可以选第二个1的，虽然它和前一个1相同。
因为前一个1被选过了，它在本轮已经被第一条规则修掉了，所以第二轮中第二个1是可选的。

## 代码
```js

const permuteUnique = (nums) => {
  const res = [];
  const len = nums.length;
  const used = new Array(len);
  nums.sort((a, b) => a - b); // 升序排序

  const dfs  = (path) => {
    if (path.length == len) { // 个数选够了
      res.push(path.slice()); // path的拷贝 加入解集
      return;                 // 结束当前递归 结束当前分支
    }

    for (let i = 0; i < len; i++) { // 枚举出所有的选择
      if (nums[i - 1] == nums[i] && i >= 1 && !used[i - 1]) { // 避免产生重复的排列
        continue;
      }
      if (used[i]) {      // 这个数使用过了，跳过。
        continue;
      }
      path.push(nums[i]); // make a choice
      used[i] = true;     // 记录路径上做过的选择
      dfs(path);       // explore，基于它继续选，递归
      path.pop();         // undo the choice
      used[i] = false;    // 也要撤销一下对它的记录
    }
  };

  dfs([]);
  return res;
};

```

### 复杂度
时间复杂度：$O(n!)$
空间复杂度：$O(nums.size())$