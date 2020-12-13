[https://leetcode-cn.com/problems/implement-trie-prefix-tree/](https://leetcode-cn.com/problems/implement-trie-prefix-tree/)


## 代码
```js

function TrieNode (value) {
  this.value = value
  this.children = []
  this.isWordEnd = false
}

function computedIndex (c) {
  return c.charCodeAt(0) - "a".charCodeAt(0);
}

/**
 * Initialize your data structure here.
 */
var Trie = function() {
  this.root = new TrieNode(null)
};

/**
 * Inserts a word into the trie.
 * @param {string} word
 * @return {void}
 */
Trie.prototype.insert = function(word) {
  let ws = this.root
  for (let i = 0; i < word.length; i++) {
    const c = word[i]
    const currentIndex = computedIndex(c)
    if (!ws.children[currentIndex]) {
      ws.children[currentIndex] = new Trie(c)
    }
    ws = ws.children[currentIndex]
  }
  ws.isWordEnd = true
};

/**
 * Returns if the word is in the trie.
 * @param {string} word
 * @return {boolean}
 */
Trie.prototype.search = function(word) {
  let ws = this.root
  for (let i = 0; i < word.length; i++) {
    const c = word[i]
    const currentIndex = computedIndex(c)
    if (!ws.children[currentIndex]) return false
    ws = ws.children[currentIndex]
  }
  return  ws.isWordEnd
};

/**
 * Returns if there is any word in the trie that starts with the given prefix.
 * @param {string} prefix
 * @return {boolean}
 */
Trie.prototype.startsWith = function(prefix) {
  let ws = this.root
  for (let i = 0; i < prefix.length; i++) {
    const c = prefix[i]
    const currentIndex = computedIndex(c)
    if (!ws.children[currentIndex]) return false
    ws = ws.children[currentIndex]
  }
  return true
};

```

## 复杂度分析
时间复杂度：$O(L)$，L 是字符串长度， insert search startsWith 操作都是。
空间复杂度：$O(M^{L})$，L 是字符串长度，M 是字符集中字符个数，如本题中 M 就是 26。
