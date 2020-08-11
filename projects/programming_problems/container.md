---
layout: post
title: Container with Most Water
subtitle: Sorry its all C++!
bigimg: "img/programming/programming.jpg"
tags: [array, two pinter, Leetcode]
---

## **Container with Most Water**<br/>[Leetcode](https://leetcode.com/problems/container-with-most-water/)



Given n non-negative integers a1, a2, ..., an , where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

Note: You may not slant the container and n is at least 2.

![image](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/17/question_11.jpg)

```cpp
class Solution {
public:
    int maxArea(vector<int>& height) {
        
        if(height.empty()){
            return 0;
        }
        int start = 0;
        int end = height.size()-1;
        int max_area = 0;
        
        while(start < end){
            int area = min(height[start],height[end])*(end-start);
            max_area = max(max_area,area);
            
            if(height[start] < height[end]){
                start++;
            }
            
            else{
                end--;
            }
            
        }
        
        return max_area;
        
    }
};
```

###**Notes**

* Follow to pointer approach start and end
* Keep maintaining area variable while moving pointers towards each other.
* Move smaller pointer first.

