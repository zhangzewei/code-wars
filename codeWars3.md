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