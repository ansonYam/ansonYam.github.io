---
layout: post
author: ansonYam
title: 141. Linked List Cycle
tags: hash-table linked-list
---

## Problem:
> Given **head**, the head of a linked list, determine if the linked list has a cycle in it.
>
> There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the **next** pointer. Internally, **pos** is used to denote the index of the node that tail's **next** pointer is connected to. Note that **pos** is not passed as a parameter.
>
> Return **true** if there is a cycle in the linked list. Otherwise, return **false**.

## My Solution:
```
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */

/**
 * @param {ListNode} head
 * @return {boolean}
 */

// disregard the 'pos' variable, it's just the answer to the test case
var hasCycle = function(head) {  
    // edge case handling
    if (head === null ) { return false; }
    
    let myArray = [];
    while (head !== null) {
        
        // if we've reached the end of the list without tripping the return true then we can return false 
        if (head.next === null) { 
            return false; 
        }
        // if head.next already exists in array, return true;
        if (myArray.indexOf(head.next) !== -1) {
            return true; 
        } else {
            myArray.push(head.next);
        }

        head = head.next;
    }
};
```
## Notes:
This was the first time for me to see a linked list, so I had a hard time working through the problem (and other linked list problems). In short, I made a new array 'myArray' that keeps note of which values we've seen already. If node.next exists in 'myArray', we can return false. 


## Better Solution:
```
var hasCycle = function(head) {
  let fast = head;
  while (fast && fast.next) {
    head = head.next;
    fast = fast.next.next;
    if (head === fast) return true;
  }
  return false;
};
```

## Notes:
The top-voted solution in the discussion forum uses two pointers, one 'slow' and one 'fast'. The analogy is that if there are two runners on a circular track, the faster runner will eventually catch up to the slower runner. To help with understanding, we can use an example:
> [3, 2, 0, -4], pos = 1

In the order head, fast: 
- 3, 3 
- 2, 0
- 0, 2
- -4, -4 return false

Aside from the strategy itself, even the 
```while (fast && fast.next)```
is a great way of checking the next node in the list. In other problems, I was doing 
```while (head !== null)```
and it would cause an error if I looked for ```head.next.next```, as I would be at the end of the list and I would be trying to check two nodes ahead (when no such node exists). 