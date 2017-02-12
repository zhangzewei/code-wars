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

## 题目17： Isomorphic Strings
### 描述

```js
Given two strings s and t, determine if they are isomorphic.

Two strings are isomorphic if the characters in s can be replaced to get t.

All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character but a character may map to itself.

For example,
Given "egg", "add", return true.

Given "foo", "bar", return false.

Given "paper", "title", return true.

Note:
You may assume both s and t have the same length.
```

### 解法

这里讲一下我对同构字 `Isomorphic` 的理解，也就是说长度相同，并且每一个字母都能够对应上另外一个字符串中的每一个字母
举个栗子：
```js
a = 'egg';
b = 'add';
// 那么a与b的对应关系就是

mapA: { e: 'a', g: 'd' };
mapB: { a: 'e', d: 'g' };

a = 'foo';
b = 'bar';

mapA: { f: 'b', o: 'a' };
mapB: { b: 'f', a: 'o', r: 'o' };
```
从这两个栗子足以看出，第二个a,b两个字符串的对应关系明显不一致，所以他们不是同构字

```js
/**
 * @param {string} s
 * @param {string} t
 * @return {boolean}
 */
var isIsomorphic = function(s, t) {
    var mapS = {};
    var mapT = {};

    for(var i in s){
        var valueS = s[i];
        var valueT = t[i];

        if(!mapS[valueS]){
            mapS[valueS] = valueT;
        } else if(mapS[valueS] != valueT) { 
            return false;
        }

        if(!mapT[valueT]){
            mapT[valueT] = valueS;
        } else if(mapT[valueT] != valueS) { 
            return false;
        }
    }
    return true;
};
```
---

## 题目18： Valid Parentheses
### 描述

```js
iven a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.+

The brackets must close in the correct order, "()" and "()[]{}" are all valid but "(]" and "([)]" are not.
```

### 解法
这道题比较有趣的，是匹配 `(), [], {}` 三种括号是否配对
这个可以使用堆栈 `stack` 的结构来解：遇到左括号就放入堆栈之中，遇到右括号就把堆栈中的左括号取出来比较是否是一对；

```js
/**
 * @param {string} s
 * @return {boolean}
 */
var isValid = function(s) {
    if(!s) return true;

    // 使用stack還儲存左括號
    var stack = [];

    var left = ['(','[','{'];
    var right = [')',']','}'];
    var match = {
        ')':'(',
        ']':'[',
        '}':'{'
    }

    for(var i in s){
        // 左括號，放入stack
        if(left.indexOf(s[i]) > -1){
            stack.push(s[i]);  
        } 

        // 右括號，從stack取出左括號判斷是否match
        if(right.indexOf(s[i]) > -1){
            var stackStr = stack.pop();  
            if(match[s[i]] != stackStr) {
                return false;
            }
        } 
    }

    // 如果左右括號都match的話，stack應該為空
    return stack.length === 0;
};
```
---

## 题目19： Length of Last Word
### 描述

```js
Given a string s consists of upper/lower-case alphabets and empty space characters ' ', return the length of last word in the string.

If the last word does not exist, return 0.

Note: A word is defined as a character sequence consists of non-space characters only.

For example, 
Given s = "Hello World",
return 5.
```

### 解法

```js
/**
 * @param {string} s
 * @return {number}
 */
var lengthOfLastWord = function(s) {
    if(s.length === 0) return 0;
    var sList = s.split(/\s/);
    var realList = sList.filter(r => r.length !== 0);
    if(realList.length === 0) return 0;
    return realList.pop().length;
};
```
---

## 题目20： Longest Common Prefix
### 描述

```js
Write a function to find the longest common prefix string amongst an array of strings.
```

### 解法

1.比對前兩個字串，從頭開始取出相同的部分為共同字首
2.後面的字串只要與目前的共同字首比對即可
3.['abcd','abccc','abdec'] ，一開始'abcd','abccc'共同字首前3碼'abc'
4.接下來只要將'abc','abdec'做比對，發現剩下'ab'，也就是最長的共同字首

```js
/**
 * @param {string[]} strs
 * @return {string}
 */
var longestCommonPrefix = function(strs) {
    if(strs == null || strs.length == 0) return "";

    // same表示目前發現的共同字首，一開始為strs[0]
    var same = strs[0];

    // 只需要比對same跟目前字串共同的字元就好
    for(var i = 1 ; i<strs.length ; i++){
        var str = strs[i];

        // 取目前的字串str跟same相等的部分做為新的same
        var j = 0;
        for(; j < same.length ; j++){
           if(same[j] != str.charAt(j)){
                break;
           } 
        }
        // same與目前字串str前幾位相同，就做為新的same
        same = same.slice(0,j);
    }

    return same;
};
```
---