
## [题目](https://leetcode-cn.com/problems/plus-one/)

## 思路
倒序遍历，如果不是9，加1返回。
如果走完循环，代表数组内都为9，数组首位需扩展，添加1


## 代码
```js
var plusOne = function(digits) {
    for (let i = digits.length - 1; i >= 0; i--) {
        if (digits[i] !== 9) {
            digits[i]++;
            return digits;
        } else {
            digits[i] = 0;
        }
    }
    digits.unshift(1);
    return digits;
};
```

## 复杂度分析
时间复杂度：O(n)
空间复杂度：O(1)
