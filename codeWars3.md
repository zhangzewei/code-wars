## 题目31：Move Zeroes
### 描述

```
Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.
For example, given nums = [0, 1, 0, 3, 12], after calling your function, nums should be [1, 3, 12, 0, 0].
Note:
You must do this in-place without making a copy of the array.
Minimize the total number of operations.
```

### 解法
```
这道题的解法很简单的，换个想法就是将数组中的非零数字排在前面排好，然后将后面的位数全部换成0
首先我们需要一个index = 0；来进行计数，遍历数组，只要不是0的数字就将这个数字填写在num[index]的地方，然后index++
最后在使用这个index将数组index位置之后的所有数字变成0就好了
```

```js
/**
 * @param {number[]} nums
 * @return {void} Do not return anything, modify nums in-place instead.
 */
var moveZeroes = function(nums) {
    var index = 0;
    for(var i = 0 ; i < nums.length ; i++){
        var n = nums[i]; 
        // not zero, index++, push to array
        if(n !== 0){
            nums[index] = n;
            index++;
        }
    }

    // after index to zero
    for(index ; index < nums.length ; index++){
        nums[index] = 0;
    }
};
```

## 拓展
### 描述

```
Given an array and a value, remove all instances of that value in place and return the new length.

Do not allocate extra space for another array, you must do this in place with constant memory.

The order of elements can be changed. It doesn't matter what you leave beyond the new length.

Example:
Given input array nums = [3,2,2,3], val = 3

Your function should return length = 2, with the first two elements of nums being 2.
```

### 解法
```
这个函数应该是上面那个函数的高级版本，传任意参数进去都行
```

```js
/**
 * @param {number[]} nums
 * @param {number} val
 * @return {number}
 */
function  removeElement(nums, val) {
    if (nums.length === 0) return nums.length;
    if (!nums.includes(val)) return nums.length;
    var count = 0;
    for (var i = 0; i < nums.length; i++) {
        if(nums[i] !== val) {
            nums[count] = nums[i];
            count++;
        }
    }
    return count;
}
```
---

## 题目32：Intersection of Two Arrays
### 描述

```
Given two arrays, write a function to compute their intersection.

Example:
Given nums1 = [1, 2, 2, 1], nums2 = [2, 2], return [2].

Note:
Each element in the result must be unique.
The result can be in any order.
```

### 解法
```
寻找两个数组之间的相同处；这个我们先比较两个数组的长度，用长度小的去作为便利的数组，因为这样便利的次数较少；
然后每次去比较长数组之中是否含有这个数字以及结果数组中是否包含这个数字；
如果长数组包含，结果集不包含，那么就把这个数字放进结果集，否则不放进
```

```js
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number[]}
 */
var intersection = function(nums1, nums2) {
    var result = [];
    var store;
    var ary;  

    if(nums1.length > nums2.length){
        store = nums1;
        ary = nums2;
    } else {
        store = nums2;
        ary = nums1;
    }

    for(var i = 0 ; i < ary.length ; i++){
        var value = ary[i];
        if(store.includes(value) && !(result.includes(value))){
            result.push(value);
        }
    }
    return result;
};
```
---


## 题目33：Majority Element
### 描述

```
Given an array of size n, find the majority element. The majority element is the element that appears more than
⌊ n/2 ⌋ times.

You may assume that the array is non-empty and the majority element always exist in the array.
```

### 解法
```
找到一个数字出现在这个数组中的次数为N/2，这个很简单，只需要建立一个Map来表示一个数字与出现次数的关系就好，把数组便利之后，
将当前数字放入map，如果是第一次放入，则这个数字对应的次数为1，如果出现过，则将对应的数字加1
```

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var majorityElement = function(nums) {
    var map = {};
    var numsLength = nums.length;
    if (numsLength === 1) return nums[0];
    for (var i = 0; i < numsLength; i++) {
        if (!map[nums[i]]) {
            map[nums[i]] = 1;
        } else {
            map[nums[i]]++;
            if (map[nums[i]] >= numsLength / 2) {
                return nums[i];
            }
        }
    }
};
```

## 拓展
### 描述

```
Given an array of integers, find if the array contains any duplicates. Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.
```

### 解法
```
这个完全就可以沿用上面所讲的，只需要出现次数为2，就返回true，否则返回false
```

```js
/**
 * @param {number[]} nums
 * @return {boolean}
 */
var containsDuplicate = function(nums) {
    var map = {};
    var numsLength = nums.length;
    if (numsLength <= 1) return false;
    for (var i = 0; i < numsLength; i++) {
        if (!map[nums[i]]) {
            map[nums[i]] = 1;
        } else {
            map[nums[i]]++;
            if (map[nums[i]] === 2) {
                return true;
            }
        }
    }
    return false;
};
```
---

## 题目34：Pascal's Triangle
### 描述

```
Given numRows, generate the first numRows of Pascal's triangle.

For example, given numRows = 5,
目标很明确，就是形成这样一个三角形的数列
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
```

### 解法
```
1. 首先当前列的数列下标n位置的值为上一列n位置的值加上上一列n+1位置的值
2. 每一列初始值都为1
3. 如果上一列n+1位置不存在则值为0
```

```js
/**
 * @param {number} numRows
 * @return {number[][]}
 */
var generate = function(numRows) {
    if (numRows === 0) return [];
    var triangle = [[1]]; // 初始化整个三角形第一列
    for (var i = 1; i < numRows; i++) {
        var prevRow = triangle[i - 1]; // 取出前一列进行遍历
        var currentRow = [1]; // 初始化现在这一列
        for (var j = 0; j < i; j++) {
            var pre = prevRow[j];
            var cur =  prevRow[j + 1] ?  prevRow[j + 1] : 0;
            currentRow.push(pre+cur); 
        }
        triangle.push(currentRow);
    }
    return triangle;
};
```
## 拓展
### 描述

```
給一個指標k，回傳第k階的Pascal's三角形。

範例：
k=3，回傳[1,3,3,1]。
```

### 解法

```js
/**
 * @param {number} rowIndex
 * @return {number[]}
 */
var getRow = function(numRows) {
    var triangle = [[1]]; // 初始化整个三角形第一列
    if (numRows === 0) return triangle[numRows];
    for (var i = 1; i < numRows + 1; i++) {
        var prevRow = triangle[i - 1]; // 取出前一列进行遍历
        var currentRow = [1]; // 初始化现在这一列
        for (var j = 0; j < i; j++) {
            var pre = prevRow[j];
            var cur =  prevRow[j + 1] ?  prevRow[j + 1] : 0;
            currentRow.push(pre+cur); 
        }
        triangle.push(currentRow);
    }
    return triangle[numRows];
};
```
---

## 题目35：Two Sum
### 描述

```
Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.
Given nums = [2, 7, 11, 15], target = 9,
Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

### 解法
```
这道题非常简单，最开始的时候我的第二个循环还是从第一个数字开始计算的，但是看了别人的讨论之后发现因为之前加过了，所以第二个循环可以不需要
再从第一个开始
```

```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(nums, target) {
    for (var i = 0; i < nums.length; i++) {
        for (var j = i + 1; j < nums.length; j++) {
            if (nums[i] + nums[j] === target) {
                return [i, j];
            }
        }
    }
    return [];
};
```
---

## 题目36：Maximum Depth of Binary Tree
### 描述

```
Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.
```

### 解法
```
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
 使用递归的方法进行查找，比较左右子节点的大小，传回较大的那一个节点
```

```js
/**
 * @param {TreeNode} root
 * @return {number}
 */
var maxDepth = function(root) {
    return find(root); 
    // 遞迴函式
    function find(node){
        // 節點到底
        if(node === null){
            return 0;
        } 

        var deepL = 1;
        var deepR = 1;
        // 有左節點，往下一層找
        if(node.left !== null){
            deepL += find(node.left)
        }
        // 有右節點，往下一層找
        if(node.right !== null){
            deepR += find(node.right)
        }

        // 回傳較大的深度depth，給上一層節點
        return deepL > deepR ?　deepL: deepR;
    }
};
```
---

## 题目37：invert Binary Tree
### 描述

```
Invert a binary tree.

     4
   /   \
  2     7
 / \   / \
1   3 6   9
to
     4
   /   \
  7     2
 / \   / \
9   6 3   1
```

### 解法
```
这道题也是使用递归的方法，将每一个节点的子节点的左右都进行转换
```

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} root
 * @return {TreeNode}
 */
var invertTree = function(root) {
    if (root === null || (root.left === null && root.right === null)) {
        return root;
    }
    var temp = root.left;
    root.left = invertTree(root.right);
    root.right = invertTree(temp);
    return root;
};
```
---

## 题目38：Same Tree

```
Given two binary trees, write a function to check if they are equal or not.

Two binary trees are considered equal if they are structurally identical and the nodes have the same value.
```

### 解法
```
1. 首先判断这两个节点是否是空节点，是就是相等的
2. 然后再判断节点的值是否相等
3. 最后将节点的子节点继续进行比较
```
```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} p
 * @param {TreeNode} q
 * @return {boolean}
 */
var isSameTree = function(p, q) {
    if (p === null && q === null) return true;
    if ((p !== null && q === null) || (p === null && q !== null)) return false;
    if (p.val !== q.val) return false;
    return isSameTree(p.right,q.right)&&isSameTree(p.left, q.left);
};
```
---