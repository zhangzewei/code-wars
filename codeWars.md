## 题目： Climbing Stairs
### 描述
```js
You are climbing a stair case.It takes n steps to reach to the top

Each time you can either climb 1 or 2 steps. In how many distinct 
ways can you climb to the top?

Note: Given n will be a positive integer.
```

### 解法
这个问题当时拿到的时候是完全没有思路的，后面上网查询了一下这个题目，知道了使用
斐波那契数列就能够解这道题目，`F(0)=1，F(1)=1, F(n)=F(n-1)+F(n-2)（n>=2
，n∈N*）`当然百度作业帮上面也有相应的解法，套路就是

```js
题目为一次可以走一步或两步:
a[1]=1;a[2]=2;
假设i的范围为3~n（n 为楼梯数），关系式为：
a[i]=a[i-1]+a[i-2];

若题目为一次可以走一步或两步或三步：
a[1]=1;a[2]=2;a[3]=4;
假设i的范围为4~n（n为楼梯数），关系式为：
a[i]=a[i-1]+a[i-2]+a[i-3]; 
```
但是当初看到这个数列的公式，第一想法是使用递归，然后，由于堆栈溢出，失败了
再看看后面的百度作业帮的那个公式，再联想一下数列，于是想到了使用数列这样的
结构来解决

```js
/**
 * @param {number} n
 * @return {number}
 */
var climbStairs = function(n) {
    if (isNaN(n)) return -1;
    if (n<=0) return -1;
    if (n<=2) return n;
    if (n>=3) {
        var res = [1,2];
        for(var i=2;i<n;i++){  
            res[i] = res[i-1] + res[i-2];  
        }  
        return res[n-1];
    }
};
```
---

## 题目： Find the odd int
### 描述
```js
Given an array, find the int that appears an odd number of times.

There will always be only one integer that appears an odd number
 of times.
```

### 解法
这是我的解法，写的真的很丑，勿喷哦

```js
function findOdd(A) {
  //happy coding!
  let indecies = [];
  
  A.forEach(a => {
    let idx = A.indexOf(a);
    let index = [];
    while (idx !== -1) {
      index.push(idx);
      idx = A.indexOf(a, idx + 1);
    }
    indecies.push(index);
  });
  const a = indecies.filter(index => (index.length % 2 !== 0));
  return A[a[0][0]];
}
```
然后是大神的解法，使用的是位运算（说实话，还不是很懂位运算，如果有什么见解，欢迎留言）

```js
function findOdd(A) {
  //happy coding!
  return A.reduce((a, b) => a^b);
}
```
---

## 题目：You're a square!
### 描述
```js
Given an integral number, determine if it's a square number:
isSquare(-1) => false
isSquare( 3) => false
isSquare( 4) => true
isSquare(25) => true
isSquare(26) => false
```

### 解法
这道就简单了

```js
var isSquare = function(n){
  return Number.isInteger(Math.sqrt(n));
}
```
---

## 题目：Strings to numbers
### 描述
```js
You are given an array of numbers in string form. Your task is to 
convert this to an array of numbers.

Your function can only be a maximum of 30 characters long 
(not including whitespaces)! I have limited the char count 
because there is a very short and easy way to achieve this task.

Here is an example of what your function needs to return:

['1','2','3'] => [1,2,3]
Edge Cases:

1 - If your function comes up against a value that isn't a number
 its place in the array must be substituted with NaN.

2 - An empty array must return an empty array.
```

### 解法
这道题主要是有一个代码字数限制，只能在30个字符以内，使用了ES6的箭头函数

```js
var convert = a => a.map(n => n*1)
```
---

## 题目：Thinkful - List and Loop Drills: Inverse Slicer
### 描述
```js
You're familiar with list slicing in Python and know, 
for example, that:
>>> ages = [12, 14, 63, 72, 55, 24]
>>> ages[2:4]
[63, 72]
>>> ages[2:]
[63, 72, 55, 24]
>>> ages[:3]
[12, 14, 63]

write a function inverse_slice() that takes three arguments: 
a list items, an integer a and an integer b. The function should
 return a new list with the slice specified by items[a:b] excluded
For example:
>>>inverse_slice([12, 14, 63, 72, 55, 24], 2, 4)
[12, 14, 55, 24]

The input will always be a valid list, a and b will always be 
different integers equal to or greater than zero, but they may 
be zero or be larger than the length of the list.
```

### 解法
这道题也相对简单

```js
function inverseSlice(items, a, b) {
  return items.filter((item, index) => !((index >= a) && (index < b)));
}
```
---

## 题目：Get all array elements except those with specified indexes
### 描述
```js
Extend the array object with a function to return all elements
 of that array, except the ones with the indexes passed in the
  parameter.

For example:

var array = ['a', 'b', 'c', 'd', 'e'];
var array2 = array.except([1,3]);
// array2 should contain ['a', 'c', 'e'];
The function should accept both array as parameter but also a
 single integer, like this:

var array = ['a', 'b', 'c', 'd', 'e'];
var array2 = array.except(1);
// array2 should contain ['a', 'c', 'd', 'e'];
```

### 解法
我的解法

```js
Array.prototype.except = function(keys)
{
  if (typeof keys === 'number') {
    return this.filter((item, index) => index !== keys);
  }
  if (Array.isArray(keys)) {
    return this.filter((item, index) => !keys.includes(index));
  }
  return -1;
}
```
大神的解法

```js
Array.prototype.except = function(keys)
{
  if(!Array.isArray(keys)) keys = [keys];
  return this.filter((a,i) => !keys.includes(i));
}
```
---

## 题目：Sum of a Sequence [Hard-Core Version]
### 描述
```js
The task is simple to explain: simply sum all the numbers from 
the first parameter being the beginning to the second parameter
 being the upper limit (possibly included), going in steps 
 expressed by the third parameter:

sequenceSum(2,2,2) === 2
sequenceSum(2,6,2) === 12 // 2 + 4 + 6
sequenceSum(1,5,1) === 15 // 1 + 2 + 3 + 4 + 5
sequenceSum(1,5,3) === 5 // 1 + 4
If it is an impossible sequence (with the beginning being larger
 the end and a positive step or the other way around), just 
 return 0. See the provided test cases for further examples :)

Note: differing from the other base kata, much larger ranges are
going to be tested, so you should hope to get your algo optimized
and to avoid brute-forcing your way through the solution.
```

### 解法

这道题有点意思，细心的人就会发现给出的例子里面可以看出一些等差数列的影子，那么我们
就可以按照等差数列的方法来解这道题了，等差数列求和公式：（首项 + 末项）* 项数 / 2

```js
function sequenceSum(begin, end, step){
  //your code here 
  const n = Math.floor((end - begin) / step) + 1;
  if (n<0) return 0; 
  const An = begin + ((n-1) * step);
  return n * (begin + An) / 2;
}
```
注意：这里面我们需要求项数`N`和末项`An`，至于`N`怎么求的，那就要靠自己去发现规律

---

## 题目：Array.prototype.size()
### 描述
```js
Implement Array.prototype.size() - without .length !

Implement Array.prototype.size(), which should simply return
the length of the array. But do it entirely without using
Array.prototype.length!
Where .length is a property, .size() is a method.

Rules

Because it is quite impossible to disable [].length, and because
filtering for "length" is an iffy proposition at best,
THIS KATA WORKS ON THE HONOUR SYSTEM.
You may cheat. But you may have trouble sleeping. Or $DEITY may
kill a puppy.

You need not support sparse arrays (but you may!). All testing
will be done with dense arrays.
Values will not be undefined. You need only support actual, real
arrays.

Your method needs to be read only. Arguments must be ignored. The
this object must not be modified.


```

### 解法
我的解法

```js
Array.prototype.size = function () {
  var i = 0;
  while (this[i] !== undefined) i++;
  return i;
};
```
大神的解法

```js
Array.prototype.size = function() {
  return this.reduce(r => r + 1, 0);
};
```
在这里看了下大神的解法，让我对reduce函数又有了新的理解

---

## 题目：Find the smallest integer in the array
### 描述
```js
Find the smallest integer in the array.

Given an array of integers your solution should find the smallest
integer. For example:
Given [34, 15, 88, 2] your solution will return 2
Given [34, -345, -1, 100] your solution will return -345

You can assume, for the purpose of this kata, that the supplied
array will not be empty.
```

### 解法
我的解法

```js
function findSmallestInt(args) {
  return args.sort((a, b) => {
    return a - b;
  })[0];
}
```
大神的解法

```js
function findSmallestInt(args) {
  return Math.min(...args);
}
```
---

## 题目：Replace With Alphabet Position
### 描述
```js
Welcome. In this kata you are required to, given a string,
replace every letter with its position in the alphabet. If 
anything in the text isn't a letter, ignore it and don't 
return it. a being 1, b being 2, etc. As an example:

alphabet_position("The sunset sets at twelve o' clock.")
Should return "20 8 5 19 21 14 19 5 20 19 5 20 19 1 20 20 23 
5 12 22 5 15 3 12 15 3 11" (As a string.)
```

### 解法
我的解法

```js
function alphabetPosition(text) {
  let alphabet = {};
  let arr = [];
  const lowCaseText = text.toLowerCase();
  for (let i = 0; i < 26; i++) {
    alphabet[(String.fromCharCode((65+i))).toLowerCase()] = (i + 1);
  }
  for (let j = 0; j < text.length; j++) {
    if (alphabet[lowCaseText[j]]) {
      arr.push(alphabet[lowCaseText[j]]);
    }
  }
  return arr.join(' ');
}
```
大神的解法

```js
function alphabetPosition(text) {
  var result = "";
  for (var i = 0; i < text.length; i++){
    var code = text.toUpperCase().charCodeAt(i)
    if (code > 64 && code < 91) result += (code - 64) + " ";
  }

  return result.slice(0, result.length-1);
}
```
---

## 题目：GetSum
### 描述
```js
Given two integers, which can be positive and negative, find the
 sum of all the numbers between including them too and return it. 
 If both numbers are equal return a or b.

Note! a and b are not ordered!

Example: 
GetSum(1, 0) == 1   // 1 + 0 = 1
GetSum(1, 2) == 3   // 1 + 2 = 3
GetSum(0, 1) == 1   // 0 + 1 = 1
GetSum(1, 1) == 1   // 1 Since both are same
GetSum(-1, 0) == -1 // -1 + 0 = -1
GetSum(-1, 2) == 2  // -1 + 0 + 1 + 2 = 2
```

### 解法
依然是等差数列

```js
function GetSum( a,b ) {
  //Good luck!
  return (a + b) * (Math.abs(b - a) + 1) / 2;
}
```
---

## 题目：Add Two Numbers
### 描述
```js
You are given two linked lists representing two non-negative 
numbers. The digits are stored in reverse order
and each of their nodes contain a single digit. Add the two 
numbers and return it as a linked list.

Input: (2 -> 4 -> 3) + (5 -> 6 -> 4) Output: 7 -> 0 -> 8
```

### 解法
[javascript linked list structure](http://www.i-programmer.info/programming/javascript/5328-javascript-data-structures-the-linked-list.html)

linked list 是一种链表结构，用于存储数字类似于：

```js
// 807这个数字的存储结构
var num8 = {
  val: 8,
  next: null,
}

var num0 = {
  val: 0,
  next: num8,
}

var num7 = {
  val: 7,
  next: num0,
}
// 807这个数字就能够用这样的结构得到
```

就只是用一個新的linked list來儲存相加後的結果
要注意的就是list1跟list2長度可能不一樣
另外就是相加後可能比9還大，需要考慮進位的情況

```js
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
var addTwoNumbers = function(l1, l2) {
    var list = new ListNode(0); //儲存輸出的結果，因為list的指針要不斷往後移，因此用一個假節點方便操作
    var result = list; // 使用一個ListNode來儲存相加的結果

    var sum,carry = 0; // carry用來處理進位

    //當 list1, list2 都沒有值，而且carry也為0的時候才結束迴圈
    while(l1 || l2 || carry > 0){
        sum = 0;

        // list1與list2長度可能不同，分開處理
        if(l1!== null){
            sum += l1.val;
            l1 = l1.next;
        }

        if(l2!==null){
            sum += l2.val;
            l2 = l2.next;
        }

        // 如果之前有進位，carry = 1；沒有的話carry = 0
        sum += carry;
        list.next = new ListNode(sum%10); //相加如果超過9，只能留下個位數放入結果list，十位數的地方進位
        carry = parseInt(sum/10);

        // list指標向後
        list = list.next;
    }
    // 因為第一個節點為假節點，跳過
    return result.next;
}
```

```js
// The complete code for the List constructor is:
function List() {
 List.makeNode = function() { 
  return {data: null, next: null}; 
 }; 
 
 this.start = null; 
 this.end = null; 
 
 this.add = function(data) { 
  if (this.start === null) { 
   this.start = List.makeNode(); 
   this.end = this.start; 
  } else { t
   this.end.next = List.makeNode(); 
   this.end = this.end.next; 
  } ; 
  this.end.data = data; 
 }; 

 this.delete = function(data) { 
  var current = this.start; 
  var previous = this.start; 
  while (current !== null) { 
   if (data === current.data) { 
    if (current === this.start) { 
     this.start = current.next; 
     return; 
    } 
    if (current === this.end) 
                      this.end = previous;
    previous.next = current.next; return; 
    }
    previous = current; 
    current = current.next; 
   }
 }; 

 this.insertAsFirst = function(d) { 
  var temp = List.makeNode(); 
  temp.next = this.start; 
  this.start = temp; 
  temp.data = d; 
 }; 

 this.insertAfter = function(t, d) { 
  var current = this.start; 
  while (current !== null) { 
   if (current.data === t) { 
    var temp = List.makeNode();
    temp.data = d; 
    temp.next = current.next; 
    if (current === this.end) this.end = temp;
    current.next = temp; 
    return; 
   } 
   current = current.next; 
   }
  };

  this.item = function(i) { 
   var current = this.start; 
   while (current !== null) { 
    i--; 
    if (i === 0) return current; 
    current = current.next; 
   } 
   return null; 
  }; 

 this.each = function(f) {
  var current = this.start;
  while (current !== null) { 
   f(current); 
   current = current.next; 
  } 
 };
} 
```
---

## 题目：Reverse String
### 描述

```js
Write a function that takes a string as input and returns the string reversed.
Example: Given s = "hello", return "olleh".
```

### 解法
我的解法

"hello" -> ['h','e','l','l','o'] -> 'o'+'l'+'l'+'e'+'h'

```js
var reverseString = function(s) {
    var result = "";
    var ary = s.split("");

    for(var i = ary.length-1 ; i >= 0 ; i--){
        result = result + ary[i];
    }
    return result;
};
```
进阶解法
> 未交換前 ['h','e','l','l','o']
第1次交換 ['h','e','l','l','o'] o,h互換 ['o','e','l','l','h']
第2次交換 ['o','e','l','l','h'] e,l互換 ['o','l','l','e','h']

```js
var reverseString = function(s) {
    var result = "";
    var ary = s.split("");
    for(var i = 0, max = (ary.length-1)/2 ; i < max   ; i++){
        var temp = ary[i];
        ary[i] = ary[ary.length - 1 - i];
        ary[ary.length - 1 - i] = temp;
    }
    return ary.join("");
};
```
---


## 题目：Valid Anagram
### 描述

```js
Given two strings s and t, write a function to determine if t is 
an anagram of s.

For example,
s = "anagram", t = "nagaram", return true.
s = "rat", t = "car", return false.

Note:
You may assume the string contains only lowercase alphabets.

Follow up:
What if the inputs contain unicode characters? How would you 
adapt your solution to such case?
```

### 解法
我的解法

> 要比較兩個字串裡面的字元是否相同，首先可以判斷長度是否相等，不相等就可以直接判定
為false 接下來將重新排序後的字串比較是否相等。

```js
/**
 * @param {string} s
 * @param {string} t
 * @return {boolean}
 */
var isAnagram = function(s, t) {
    if(s.length !== t.length) return false;

    var s1 = s.split("").sort().join("");
    var t1 = t.split("").sort().join("");

    return s1 === t1;
};
```
---

## 题目： Excel Sheet Column Number
### 描述

```js
Related to question Excel Sheet Column Title
Given a column title as appear in an Excel sheet, return its corresponding column number.
For example:
A -> 1
B -> 2
C -> 3
...
Z -> 26
AA -> 27
AB -> 28 
```

### 解法

A-Z總共26個字母，因此這就是一個26進位的系統

將字串分別取出字元A-Z，根據ANSI CODE，A的code為65，A = 65 - 64 = 1

以AB為例， AB = (A)26^1 + (B)26^0 = 1*26 + 2*1 = 28

以AZ為例， AZ = (A)26^1 + (Z)26^0 = 1*26 + 26*1 = 52

```js
/**
 * @param {string} s
 * @return {number}
 */
var titleToNumber = function(s) {
    var sum = 0;
    var exp = 0;
    for(var i = s.length -1 ; i >= 0 ; i--){
        // 根據ansi將字成數字，从字串后面，也就是低位數開始取
        var v = s.charCodeAt(i) - 64;
        // 毎多一个字代表26的n次方
        v = v*Math.pow(26,exp++);
        sum += v;
    }
    return sum;    
};
```
---