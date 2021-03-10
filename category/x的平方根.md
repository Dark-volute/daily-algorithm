[https://leetcode-cn.com/problems/sqrtx/](https://leetcode-cn.com/problems/sqrtx/)

## 代码
```js

const mySqrt = function(x) {
    if (x < 2) return x
    let left = 1, mid, right = x
    while (left <= right) {
       mid = Math.floor(left + (right - left) / 2)
       if (mid * mid === x) return mid
       if (mid * mid < x) {
           left = mid + 1
       }else {
           right = mid - 1
       }
    }
    return right
}

```

## 复杂度分析

时间复杂度：$O(logN)$
空间复杂度：$O(1)$

