## nk1：构造回文
### 描述

```
给定一个字符串s，你可以从中删除一些字符，使得剩下的串是一个回文串。如何删除才能使得回文串最长呢？
输出需要删除的字符个数。
输入描述:
输入数据有多组，每组包含一个字符串s，且保证:1<=s.length<=1000.
输出描述:
对于每组数据，输出一个整数，代表最少需要删除的字符个数。
```

### 解法
```
这道题就是动态规划求最大子集的变形，将一个字符串正序和倒序来一次就行了，但是不知道为什么我的函数在题目上的编辑器里不能够通过。。。
```

```js
var _lcs = function(str) {
    var table = [];
    for (var i = 0; i < str.length + 1; i++) {
        table[i] = [];
        for (var j = 0; j < str.length + 1; j++) {
            table[i][j] = 0;
        }
    }
    for (var a = 1; a < str.length + 1; a++) {
      for (var b = 1; b < str.length + 1; b++) {
        if (str[a] === str[str.length + 1 - b]) {
          table[a][b] = table[a - 1][b - 1] + 1;
        } else if (table[a - 1][b] >= table[a][b]) {
          table[a][b] = Math.max(table[a - 1][b], table[a][b - 1]);
        }
      }
    }
    return table[str.length][str.length];
};
```
---