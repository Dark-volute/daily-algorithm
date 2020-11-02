
[https://leetcode-cn.com/problems/shortest-distance-to-a-character/](https://leetcode-cn.com/problems/shortest-distance-to-a-character/)

## 暴力破解
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
