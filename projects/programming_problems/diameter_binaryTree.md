---
layout: post
title: Diameter of a Binary Tree
subtitle: Sorry its all C++!
bigimg: "img/programming/programming.jpg"
tags: [Binary Tree]
---

## **Diameter of a Binary Tree** <br/> [Leetcode](https://leetcode.com/problems/diameter-of-binary-tree/)

Given a binary tree, you need to compute the length of the diameter of the tree. The diameter of a binary tree is the length of the longest path between any two nodes in a tree. This path may or may not pass through the root.

```cpp
/**
* Definition for a binary tree node.
* struct TreeNode {
*     int val;
*     TreeNode *left;
*     TreeNode *right;
*     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
* };
*/
class Solution {
public:

    int height_util(TreeNode* node, int& max_path){
        if(node == NULL){
            return 0;
        }


        int l_height = height_util(node->left,max_path); //height of left subtree
        int r_height = height_util(node->right,max_path); // height of right subtree
        int path_length = l_height + r_height + 1; //longest path will have the max sum of height of left and right subtree

        if(path_length > max_path){
            max_path = path_length;
        }

        return 1 + max(l_height,r_height);

    }

    int diameterOfBinaryTree(TreeNode* root) {

        if(root == NULL){
            return 0;
        }
        int max_path = -1;
        auto ht = height_util(root, max_path);
        return max_path - 1;
    }
};
```
