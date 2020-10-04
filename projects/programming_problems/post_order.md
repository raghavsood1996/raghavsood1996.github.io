---
layout: post
title: Iterative Post-order Traversal
subtitle: Sorry its all C++!
bigimg: "img/programming/programming.jpg"
tags: [Binary Tree]
---

## **Binary Tree Postorder Traversal**</br>[Leetcode](https://leetcode.com/problems/binary-tree-postorder-traversal/)

Given the root of a binary tree, return the postorder traversal of its nodes' values.

```cpp
class Solution {
public:
  
    vector<int> postorderTraversal(TreeNode* root) {
        
        if(root == NULL){
            return{};
        }
        vector<int> traversal;
        stack<TreeNode*> st;
        unordered_map<TreeNode*,bool> visited;
        st.push(root);
        while(!st.empty()){
            auto node = st.top();
            st.pop();
            if(visited[node]){
                traversal.push_back(node->val);
                continue;
            }
            
            if(node != NULL){
                visited[node] = 1;
                st.push(node);
            }
            
            if(node->right != NULL){
                st.push(node->right);
            }
            
            if(node->left != NULL){
                st.push(node->left);
            }
        }
        return traversal;
    }
};
```

### Notes

* Traversal using explicit stack.
* Maintain a visited variable and push the elements in the stack in opposite order of recursion.
* Use a variable if it is visited when popped from stack.