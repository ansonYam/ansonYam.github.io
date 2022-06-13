---
layout: post
author: ansonYam
title: 509. Fibonacci Number
tags: dynamic-programming
---

## Problem:
> The **Fibonacci numbers**, commonly denoted `F(n)` form a sequence, called the **Fibonacci sequence**, such that each number is the sum of the two preceding ones, starting from `0` and `1`. That is,
```
F(0) = 0, F(1) = 1
F(n) = F(n - 1) + F(n - 2), for n > 1
```
> Given `n`, calculate `F(n)`.

## Solution:
```
/**
 * @param {number} n
 * @return {number}
 */
let memo = [];

var fib = function(n) {
    // memoization (top-down)
    /**
    if (n === 0 || n === 1) { // base cases
        return n;
    }
    if (!memo[n]) {
        memo[n] = fib(n - 1) + fib(n - 2);
    }
    return memo[n];
    */
    
    // tabulation (bottom-up)
    let F = new Array();
    F[0] = 0;
    F[1] = 1;
    for (let i = 2; i <= n; i++) {
        F[i] = F[i - 1] + F[i - 2];
    }
    return F[n];  
    
};
```

## Notes:
> I completed this by following the pseudocode on the [Leetcode Explore](https://leetcode.com/explore/featured/card/dynamic-programming/630/an-introduction-to-dynamic-programming/4035/) page; both a bottom-up and a top-down soluation are supplied.
> To go over dynamic programming principles, really for myself more than anything else: 
> Dynamic programming is a problem-solving method in which you break down a large problem into smaller 'subproblems', for example we noted above that `F[3] = F[2] + F[1]` in the Fibonacci sequence. The hard part seems to be recognizing the appropriate subproblem...
> The two ways to implement a DP solution are 
1. Bottom-up
2. Top-down
>
> Going back to the solution code, in the bottom-up solution we calculate `F[1]`, then `F[2]`, etc., while logging the results in our F array. 
> For the top-down solution, we calculate `F[n]` by summing `F[n-1] + F[n-2]`, which triggers a recursion loop (to calculate `F[n-1]`, we need `F[n-2] and F[n-3]`, and this continues until we reach `F[0]` and `F[1]`).
> To save time on the top-down solution, we can use something called 'memoization', or 'writing it down'. 
> Here I've shamelessly ripped a diagram straight from the Leetcode page: 
![Fibonacci tree](/assets/img/fib_tree.png)
> We can see that with the top-down solution, we would need to re-calculate `F[2]` several times. This can be avoided by storing the result of `F[2]` in a 'memo' hashmap. 