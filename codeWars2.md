## 题目16： Reverse Vowels of a String
### 描述

```js
Write a function that takes a string as input and reverse only the vowels of a string.

Example 1:
Given s = "hello", return "holle".

Example 2:
Given s = "leetcode", return "leotcede".

Note:
The vowels does not include the letter "y".
```

### 解法
1. 先将字符串变为数组，然后取出其中的元音字母;
2. 用之前的取出的元音字母，倒序放回字符串数组;
3. 将字符串数组变为字符串;
4. `/^[aeiou]$/i`这个正则表达式的意思是匹配从aeiou开头到最后不区分大小写的字母

```js
/**
 * @param {string} s
 * @return {string}
 */
var reverseVowels = function(s) {
    var vowels = [];  

    for(var i = 0 ; i< s.length ; i++){
        if((/^[aeiou]$/i).test(s[i])){
            vowels.push(s[i]);
        }    
    }

    var v = vowels.length - 1;

    var sAry = s.split("");


    for(var j = 0 ; j < sAry.length ; j++){
        if((/^[aeiou]$/i).test(sAry[j])){
            sAry[j] = vowels[v--];
        }    
    }

    return sAry.join("");
};
```
---
