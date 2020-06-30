---
layout: post
title: Search Insert Position
subtitle: Sorry its all C++!
bigimg: "img/snow.jpg"
tags: [array, binary search, Leetcode]
---

## **Search Insert Position** <br/> [Leetcode](https://leetcode.com/problems/search-insert-position/)


Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You may assume no duplicates in the array.

```cpp
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        int low = 0;
        int high = nums.size() - 1;
        
        while(low <= high){
            int mid = low + (high- low)/2;
            
            if(target > nums[mid]){
                
                if(mid == nums.size() -1){
                    return nums.size();
                }
                
                low = mid + 1;
            }
            
            else{
                
                if(mid == 0 || nums[mid-1] < target){
                    return mid;
                }
                
                high = mid -1;
            }
        }
        
        return -1;
            
        }
        
    
};
```

### **Notes**

* Binary Search with a little modification.
* Be aware of the corner cases at start and end of the array.
