---
layout: post
author: ansonYam
title: 701. Insert into a Binary Tree
tags: tree
---

## Problem:
> You are given the **root** node of a binary search tree (BST) and a **value** to insert into the tree. Return *the root node of the BST after the insertion.* It is guaranteed that the new value does not exist in the original BST.
>
> Notice that there may exist multiple valid ways for the insertion, as long as the tree remains a BST after insertion. You can return any of them.

## Better Solution:
```
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @param {number} val
 * @return {TreeNode}
 */

var insertIntoBST = function(root, val) {   
    let newNode = new TreeNode(val);

    function traverse(node) {
        if(node === null) return newNode;

        if (newNode.val < node.val) {
            if (node.left === null) {
                node.left = newNode;
            } else {
                traverse(node.left);
            }
        } else {
            if (node.right === null) {
                node.right = newNode;
            } else {
                traverse(node.right);
            }
        }
        return node;
    }
    
    return traverse(root);
};
```

## Notes:
At this point in the module, I was fully out of my depth, having not properly understood binary search trees. I had to turn to the discussion forum for a solution. As it turns out, there is a special property of BST that nodes on the right subtree should be greater than the root, while nodes on the left subtree should be less than the root value. In the future I will have to become more familiar with recursive solutions. 