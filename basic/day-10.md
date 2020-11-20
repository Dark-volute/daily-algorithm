[https://leetcode-cn.com/problems/two-sum](https://leetcode-cn.com/problems/two-sum)

## 思路
利用hashmap 遍历一次

## 代码
```js
const twoSum = (nums, target) => {
  // 1. 构造哈希表
  const map = new Map();

  // 2. 遍历数组
  for (let i = 0; i < nums.length; i++) {
    // 2.1 如果找到 target - nums[i] 的值
    if (map.has(nums[i])) {
      return [map.get(nums[i]), i];
    } else {
      // 2.2 如果没找到则进行设置
      map.set(target - nums[i], i);
    }
  }
};
```

## 复杂度分析
时间复杂度：$O(N)
空间复杂度：$O(N)