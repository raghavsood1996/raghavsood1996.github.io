---
layout: post
title: Permutations
subtitle: Sorry its all C++!
bigimg: "img/programming/programming.jpg"
tags: [Recursion, Auxillary Buffer,Leetcode]
---

## **Permutations**<br/>[Leetcode](https://leetcode.com/problems/permutations/)

Given a collection of distinct integers, return all possible permutations.

```cpp
class Solution {
public:
    vector<vector<int>> perms; //strores output
    unordered_map<int,bool> in_buffer; // to track what is already in the buffer
    
    //helper function to copy buffer to output
    void add_perm(vector<int> &buffer){
        vector<int> perm;
        for(auto i : buffer){
            perm.push_back(i);
        }
        perms.push_back(perm);
    }
    
    //REcursive Function to fill inthe buffer
    void perm_help(vector<int> &nums, vector<int> &buffer, int buffer_idx){
        if(buffer_idx >= nums.size()){
            add_perm(buffer); //when full add to result
            return;
        }
        
        for(int i = 0 ; i< nums.size();i++){ // iterate through all the possible candidates
            if(in_buffer[nums[i]]){
                continue; // do not consider what is already in the buffer
            }
            
            buffer[buffer_idx] = nums[i];
            in_buffer[nums[i]] = true;
            
            perm_help(nums, buffer, buffer_idx+1); // recure to next buffer
            in_buffer.erase(buffer[buffer_idx]); // reset the bufffer
            
        }
    }
    
    vector<vector<int>> permute(vector<int>& nums) {
        
        vector<int> buffer(nums.size());
        
        perm_help(nums, buffer, 0);
        
        return perms;
    }
};
```

### **Notes**

* Follow the Auxillary Buffer Technique.
* Keep filling in the buffer recursively.
* Also keep track of what is already in the buffer using a map.
