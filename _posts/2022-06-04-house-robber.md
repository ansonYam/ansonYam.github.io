---
layout: post
author: ansonYam
title: 198. House Robber
tags: dynamic-programming
---

## Problem:
> You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security systems connected and it will automatically contact the police if two adjacent houses were broken into on the same night.
> 
> Given an integer array `nums` representing the amount of money of each house, _return the maximum amount of money you can rob tonight **without alerting the police.**_

## Solution:
```
/**
 * @param {number[]} nums
 * @return {number}
 */
var rob = function(nums) {
    // we are picking between robbing house 0 + max of houses (2:n) and max of robbing house (1:n)
    let oneBefore = twoBefore = 0; 
    for (let i = 0; i < nums.length; i++) {
        let temp = Math.max(nums[i] + twoBefore, oneBefore);
        
        // shift everything forwards one space
        twoBefore = oneBefore;
        oneBefore = temp;
    }
    return oneBefore;
};
```

## Notes:
> I completed this by following the pseudocode on the [Leetcode Explore](https://leetcode.com/explore/featured/card/dynamic-programming/630/an-introduction-to-dynamic-programming/4094/) page. 
>
> Common DP problems include asking for the optimum value of something (max. or min.), or the number of ways to do something (e.g. climb stairs). This is one such problem (maximum amount stolen).
> Reading from the Leetcode page, a greedy algorithm fails here. For example, if we are to take the testcase `[2,7,9,3,1]`, we would normally break the problem down into checking the first two elements `[2,7]`, and then the next two, and so on. But as we cannot rob adjacent houses, choosing `[7]` from `[2,7]` will prevent us from taking the `[9]` house. 
> 
> Usually, if earlier decisions affect future decisions, it is a DP problem. 
>
> Onto the solution:
> Let's look for some subproblems. As adjacent house are not allowed, we actually need quite a large array, for example `[1,2,3,1]`.
> If we choose to rob `[1]`, it forces us to skip `[2]`, but now we can pick between `[3]` and `[1]`. We can choose `[1,3]` here as it has the higher sum. How about skipping `[1]` and robbing `[2]` instead? Only one choice, it has to be `[1]`. So we can compare `[1,3]` and `[2,1]`, `[1,3]` is our winner. 
>
> For a visual representation, another shamelessly ripped screenshot, this time from [Neetcode](https://www.youtube.com/watch?v=73r3KWiEvyk):
> ![Image](/assets/img/neetcode-house-robber.png)
>
> We can maybe see that a potential subproblem would be the max of just starting from `[1]`. Another would be the subproblem of starting from `[2]`.   
> In pseudocode, `rob = max(arr[0] + rob[2:n], rob[1:n])`. We are comparing the case where we rob the first house against the case where we rob the second house. To evaluate `rob[1:n]` we will loop back into `rob = max(arr[1] + rob[3:n]`, and so on. So we have a recursion here. 
>
> I actually think it makes more sense to work backwards, but I'll follow the Neetcode video for now and tabulate left to right (this is a bottom-up strategy, if I'm not mistaken).
> `[1,2,3,1]` can be replaced with the maximum robbery amount for each subarray so far. At index 0, the maximum amount will just be 1. At index 1, the maximum amount will be skipping the `[1]` and robbing the `[2]`, so 2. At index 2, the maximum is robbing `[1,3]`, or 4. So far we have `[1,2,4,?]`. How about that last maximum? To find it, we have to compare between the maximum one index behind (4) and summing the current element with the maximum two indices behind (1 + 2). The maximum remains 4. So our completed array is `[1,2,4,4]`. 