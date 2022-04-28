---
layout: post
author: ansonYam
title: 88. Merge Sorted Array
tags: array sorting
---

## Problem:
> You are given two integer arrays nums1 and nums2, sorted in non-decreasing order, and two integers m and n, representing the number of elements in nums1 and nums2 respectively.
>
> Merge nums1 and nums2 into a single array sorted in non-decreasing order.
>
> The final sorted array should not be returned by the function, but instead be stored inside the array nums1. To accommodate this, nums1 has a length of m + n, where the first m elements denote the elements that should be merged, and the last n elements are set to 0 and should be ignored. nums2 has a length of n

## My Solution:
```
/**
 * @param {number[]} nums1
 * @param {number} m
 * @param {number[]} nums2
 * @param {number} n
 * @return {void} Do not return anything, modify nums1 in-place instead.
 */
var merge = function(nums1, m, nums2, n) {
    let j = 0; 
    for(let i = m; i < nums1.length; i++) {
        nums1[i] = nums2[j];
        j++;
    }
    nums1.sort(function(a,b){return a-b});
};
```

## Notes:
This was a pretty beginner-friendly problem, not only were the two arrays sorted for me, nums1 was already the right size to accept the elements from nums2. Anyways, all I did was loop through the second array (nums2), overwriting the given 0s in nums1 with the appropriate element. The sorting was a bit confusing, as I tried the native .sort() function and it gave a wrong result. As it turns out, .sort() treats its values as strings by default, sorting in ascending alphabetical order, so an input of
> [-10,-10,-9,-9,-9,-8,-8,-7,-7,-7,-6,-6,-6,-6,-6,-6,-6,-5,-5,-5,-4,-4,-4,-3,-3,-2,-2,-1,-1,0,1,1,1, ...]

gave an output of 

> [-1,-1,-1,-1,-1,-10,-10,-10,-10,-2,-2,-2,-2,-2,-2,-2,-2,-2,-3,-3,-3,-3,-3,-4,-4,-4,-4, ...]

which was not correct. Instead, .sort() takes in an optional 'compareFunction' that can be used to define sort order. Per [w3schools](https://www.w3schools.com/jsref/jsref_sort.asp), 
> The function should return a negative, zero, or positive value, depending on the arguments: 
``` function(a, b){return a-b} ```
> When sort() compares two values, it sends the values to the compare function, and sorts the values according to the returned (negative, zero, positive) value.