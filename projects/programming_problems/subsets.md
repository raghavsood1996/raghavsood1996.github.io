---
layout: post
title: Subsets
subtitle: Sorry its all C++!
bigimg: "img/programming/programming.jpg"
tags: [recursion, auxilary buffer, Leetcode]
---

## **Subsets**<br/>[Leetcode](https://leetcode.com/problems/subsets/)
Given a set of distinct integers, nums, return all possible subsets (the power set).

Note: The solution set must not contain duplicate subsets.

```cpp
class Solution {
public:
    
    vector<vector<int>> all_subsets;
    
    void add_subset(vector<int> &buff, int buff_idx){
        
        vector<int> set;
        
        for(int i=0;i <buff_idx;i++){
            
            set.push_back(buff[i]);
        }
        
        all_subsets.push_back(set);
    }
    
    void compute_subsets(vector<int> &nums, vector<int> &buff, int buff_idx, int start_idx){
        
        add_subset(buff,buff_idx);
        
        if(buff_idx == buff.size() || start_idx == nums.size()){
             
            return;
        }

        for(int i= start_idx; i< nums.size(); i++){
            
            buff[buff_idx] = nums[i] ;
            compute_subsets(nums,buff, buff_idx+1, i+1);

        }
        
        return;
    }
    
    vector<vector<int>> subsets(vector<int>& nums) {
        
        vector<int> set(nums.size());
        compute_subsets(nums,set,0,0);
        
        return all_subsets;
        
    }
};
```

### **Notes**

* Recursion Question
* Auxilary Buffer technique where we add all buffers of all size