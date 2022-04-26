---
layout: post
author: ansonYam
title: 121. Best Time to Buy and Sell Stock
module: Data Structure I
---

## Problem:
> You are given an array prices where prices[i] is the price of a given stock on the ith day.
>
> You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock.
>
> Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.

## My Solution:
```
/**
 * @param {number[]} prices
 * @return {number}
 */
var maxProfit = function(prices) {
    
    /** Time limit exceeded, very sad 
    let max = 0;
    for (let i = 0; i < prices.length - 1; i++) {
        for (let j = i+1; j < prices.length; j++) {
            if (prices[j] - prices[i] > max) {
                max = prices[j] - prices[i];
            }
        }
    }
    return max;
    */ 
}
```
## Better Solution:
```
var maxProfit = function(prices) {

    let minPrice = Number.MAX_SAFE_INTEGER;
    let maxProfit = 0;
    
    for (let i = 0; i < prices.length; i++) {
        if (prices[i] < minPrice) {
            minPrice = prices[i];
        } else if (prices[i] - minPrice > maxProfit) {
            maxProfit = prices[i] - minPrice;   
        }
    }
    return maxProfit;
};
```

## Notes:
I didn't manage to solve this problem naively / via brute force, the execution timed out before I could finish the test cases. So, I adapted the Java solution from the leetcode site itself. It only passes over the prices array once, updating the minimum price and max profit only as required (can't buy stock and then sell in the past). To work through the example [7, 1, 5, 3, 6, 4]:
- i = 0, prices[0] = 7 < MAX_SAFE_INTEGER, so minPrice = prices[0] = 7
- i = 1, prices[1] = 1 < 7, minPrice = 1
- i = 2, prices[2] = 5 is not < 1, so we move into the else loop, maxProfit = prices[2] - minPrice = 5 - 1 = 4
- i = 3, prices[3] = 3 is not < 1, so we move into the else loop, prices[3] - minPrice = 3 - 1 not greater than 4, so maxProfit is unchanged

And this continues for the entire array.