
[https://leetcode-cn.com/problems/shortest-distance-to-a-character/](https://leetcode-cn.com/problems/shortest-distance-to-a-character/)

# 暴力破解
```js
var shortestToChar = function(S, C) {
    let result = []
    let min = null
    for (let i = 0; i < S.length; i++) {
         for (let j = 0; j < S.length; j++) {
             if (S[i] === C) {
                 result[i] = 0
             } else {
                 if (S[j] === C) {
                     min = (Math.abs(j - i) > min && min) ? min : Math.abs(j - i)
                     result[i] = min
                 }
             }      
     }
      min = null
    }
    return result
};
```

# 滑动窗口解法

## 代码
```
var shortestToChar = function(S, C) {
    let l  = S[0] === C ? 0 : Infinity
    let r = S.indexOf(C)
    let res = []

    for (let i = 0; i < S.length; i++) {
        // 计算字符到当前窗口左右边界的最小距离
        res[i] = Math.min(Math.abs(i - l), Math.abs(r - i))

        // 遍历完了当前窗口后，将窗口右移
        if (i === r) {
            l = r
            r = S.indexOf(C, l + 1)
        }
    }
    return res
};
```
