[https://leetcode-cn.com/problems/top-k-frequent-elements](https://leetcode-cn.com/problems/top-k-frequent-elements)

## 思路
遍历数组，统计出现频次保存在哈希表中，再进行排序。
## 代码
```js
var topKFrequent = function (nums, k) {
    const map = new Map()
    for (let i = 0; i < nums.length; i++) {
        if (map.has(nums[i])) {
            map.set(nums[i], map.get(nums[i]) + 1)
        } else {
            map.set(nums[i], 1)
        }
    }
    return [...map.entries()]
        .sort((a, b) => b[1] - a[1])
        .slice(0, k)
        .map(a => a[0]);
};
```
## 复杂度分析
时间复杂度：（logN） 排序log N
空间复杂度：O(N) 