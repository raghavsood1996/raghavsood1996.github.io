---
layout: post
title: Combinations
subtitle: Sorry its all C++!
bigimg: "img/programming/programming.jpg"
tags: [recursion, buffer, Leetcode]
---

## **Combinations** <br/>[Leetcode](https://leetcode.com/problems/combinations/)
Given two integers n and k, return all possible combinations of k numbers out of 1 ... n.

```cpp
class Solution {
public:
    
    vector<vector<int>> combinations;
    
    void rec_util(int n ,int k, vector<int> &buff,int start_idx, int buff_idx){
        if(buff_idx == k){
            vector<int> comb;
            for(int i=0;i<k;i++){
                comb.push_back(buff[i]);
            }
            
            combinations.push_back(comb);
            return;
        }
        
        if(start_idx > n){
            return;
        }
        
        for(int i=start_idx; i<=n ;i++){
            buff[buff_idx] = i;
            
            rec_util(n,k,buff,i+1, buff_idx+1);
        }
        
    }
    vector<vector<int>> combine(int n, int k) {
        
        vector<int> buff(k);
        rec_util(n,k,buff,1,0);
        
        return combinations;
    }
};
```

### **Notes**

* Recursion Question.
* Constant buffer size approach.
* Recursively fill buffer and add when full.

