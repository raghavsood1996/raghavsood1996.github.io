---
layout: post
title: Maximum Subarray
subtitle: Sorry its all C++!
bigimg: "img/programming/programming.jpg"
tags: [array, subarray,kadane, Leetcode]
---

## **Maximum Subarray** <br/> [Leetcode](https://leetcode.com/problems/maximum-subarray/)


Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

```cpp
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        
        int max_sum = INT_MIN;
        long int sum_here = INT_MIN;
        
        for(int i =0 ;i< nums.size(); i++){
            
            //maintaig max sum upto every index
            sum_here = std::max(long(nums[i]),nums[i] + sum_here);
            
            if(sum_here > max_sum){
                max_sum = sum_here;
            }
        }
        
        return max_sum;
        
    }
};
```

### **Notes**

* Subarray Problem.
* Kadane's algorithm 0(n) solution. The trick is maintaing maximum sub upto each index.
