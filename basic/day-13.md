[https://leetcode-cn.com/problems/number-of-boomerangs/submissions/](https://leetcode-cn.com/problems/number-of-boomerangs/submissions/)

## 思路
就是找出所有符合三个点x,y,z，并且dis(x,y)=dis(x,z)这种点的个数。首先要明确两点间距离怎么计算：

$$x=(x1,x2)$$

$$y=(y1,y2)$$

$$dis(x,y) = \sqrt{(x1 - y1)^{2} + (x2 - y2) ^{2}}$$

由于求的是算数平方根，所以我们算距离的时候也没必要开根号了

我们可以很容易地想到暴力解法，也就是来个三重循环

## 代码
```js
/**
 * @param {number[][]} points
 * @return {number}
 */
var numberOfBoomerangs = function(points) {
    if (!points || points.length <= 2) return 0
    let res = 0
    for (var i = 0; i < points.length; i++) {
        for (var j = 0; j < points.length; j++) {
            if (i == j) continue;
            for (var k = 0; k < points.length; k++) {
                if (k == i || k == j) continue;
                if (getDistance(points[i], points[j]) === getDistance(points[i], points[k])) {
                    res++;
                }     
            }
        }
    }
    return res
};

function getDistance(x, y) {

    let x1 = y[0] - x[0];
    let y1 = y[1] - x[1];

    return x1 * x1 + y1 * y1;
}
```

# HashMap 优化

### 思路
因为需要考虑顺序，固定一个点进行循环，每次将相同的距离次数存入map，根据规律，比如有 n 个 距离为2 ，那么可排列的组合为n*(n-1)

### 代码
```js
var numberOfBoomerangs = function(points) {
    if (!points || points.length <= 2) return 0
    let map = new Map()
    let res = 0
    for (var i = 0; i < points.length; i++) {
        for (var j = 0; j < points.length; j++) {
            if (i == j) continue;
            let dis = getDistance(points[i], points[j])
            map.set(dis, (map.get(dis) || 0) + 1)
        }
        [...map.values()].forEach(count => {
            res += count * (count - 1)
        })
        map.clear()
    }
    return res
};
```
