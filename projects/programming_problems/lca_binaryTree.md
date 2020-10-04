---
layout: post
title: Lowest Common Ancestor Binary Tree
subtitle: Sorry its all C++!
bigimg: "img/programming/programming.jpg"
tags: [Binary Tree]
---

## **Lowest Common Ancestor Binary Tree**<br/> [Leetcode](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/)

Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.

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
    TreeNode* lca_util(TreeNode* node, TreeNode* p, TreeNode* q){

        if(node == NULL){
            return NULL;
        }

        if(node->val == p->val || node->val == q->val){ 
            return node;
        }

        TreeNode* left_lca = lca_util(node->left,p,q);
        TreeNode* right_lca = lca_util(node->right, p,q);
        if(left_lca != NULL && right_lca != NULL){ // if found in both right and left subtrees then it is the lowest commmon ancestor
            return node;
        }


        return left_lca != NULL ? left_lca : right_lca; // if only found in one then return the one where it was found
    }

    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {

        return lca_util(root,p,q);
    }
};
```

### **NOTES**

* Follow the bottom to up approach.