[https://leetcode-cn.com/problems/next-greater-element-ii/](https://leetcode-cn.com/problems/next-greater-element-ii/)

## 思路

如果不考虑数组循环: 维护一个单调递减栈(存放数组索引)，遇到比栈头大的元素，出栈，然后设置当前元素即可。
考虑循环的话用一个小技巧 i % len，注意边界问题即可

## 代码
```js
/**
 * @param {number[]} nums
 * @return {number[]}
 */

// 不考虑数组循环
var nextGreaterElements = function(nums) {
    const stack = []
    const res = new Array(nums.length).fill(-1)
    for (let i = 0; i < nums.length; i++) {
        while (stack.length && nums[i] > nums[stack[stack.length - 1]]) {
            res[stack.pop()] = nums[i] 
        }
        stack.push(i)
    }

    return res
};


var nextGreaterElements = function(nums) {
    const stack = []
    const res = new Array(nums.length).fill(-1)
    const len = nums.length
    for (let i = 0; i < len * 2; i++) {
        while (stack.length && nums[i % len] > nums[stack[stack.length - 1]]) {
           
            res[stack.pop()] = nums[i % len] 
    
        }
        stack.push(i % len)
    }
    return res
};

```


### 复杂度
时间复杂度：$O(n)$
空间复杂度：$O(stack.size())$