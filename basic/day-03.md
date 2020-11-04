
[https://leetcode-cn.com/problems/decode-string/](https://leetcode-cn.com/problems/decode-string/)

## 思路
我们可以利用 stack 来实现这个操作，遍历这个字符串 s，判断每一个字符的类型：
- 如果是字母 --> 添加到 stack 当中
- 如果是数字 --> 先不着急添加到 stack 中 --> 因为有可能有多位
- 如果是 [ --> 说明重复字符串开始 --> 将数字入栈 --> 并且将数字清零
- 如果是 ] --> 说明重复字符串结束 --> 将重复字符串重复前一步储存的数字遍


## 代码
```js
var decodeString = function(s) {
    let strStack = []
    let numStack = []
    let num = 0
    let str = ''
    for (let i = 0; i< s.length; i++) {
        // 如果是次数
        if (!isNaN(s[i])) {
            // 处理二位及以上次数
            num = num * 10 + +s[i]
        } else if (s[i] === '[') {
            numStack.push(num)
            strStack.push(str)
            num = 0
            str = ''
        } else if (s[i] === ']'){
            let repeatTimes = numStack.pop() // 获取拷贝次数
            str = strStack.pop() + str.repeat(repeatTimes) 
        } else {
            str += s[i]
        }
    }
    return str
};
```

## 复杂度分析
时间复杂度：$O(N)$，其中 N 为解码后的 s 的长度。
空间复杂度：$O(N)$，其中 N 为解码后的 s 的长度。
