---
layout: post
title: Sort Colors
subtitle: Sorry its all C++!
bigimg: bigimg: "img/programming/programming.jpg"
tags: [array, DNF, Leetcode]
---

## **Sort Colors** <br/> [Leetcode](https://leetcode.com/problems/sort-colors/)

Given an array with n objects colored red, white or blue, sort them in-place so that objects of the same color are adjacent, with the colors in the order red, white and blue.

Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.

Note: You are not suppose to use the library's sort function for this problem.

```cpp
class Solution {
public:
    void sortColors(vector<int>& nums) {
        
        int start = 0;
        int end = nums.size() - 1;
        int itr  = 0;
        int pivot  = 1;
        
        //just need to go until higher boundary
        while(itr <= end){
            
            if(nums[itr] < pivot){
                std::swap(nums[itr],nums[start]);
                start++;
                itr++;
            }
            
            // do not increment itr here coz unprocessed swap
            else if(nums[itr] > pivot){
                std::swap(nums[itr],nums[end]);
                end--;
                
            }
            
            else {
                itr++;
            }
        }
        
        return;
    }
};
```

### **Notes**

* Array Partition Problem
* Use Traversal from both ends just like solving a Dutch National Flag problem.
