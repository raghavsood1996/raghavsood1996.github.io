---
layout: post
title: Rotate Image
subtitle: Sorry its all C++!
bigimg: "img/programming/programming.jpg"
tags: [Array, 2D Aray, Leetcode]
---

## **Rotate Image**<br/>[Leetcode](https://leetcode.com/problems/rotate-image/)

You are given an n x n 2D matrix representing an image.
Rotate the image by 90 degrees (clockwise).

Note:
You have to rotate the image in-place, which means you have to modify the input 2D matrix directly. DO NOT allocate another 2D matrix and do the rotation.

```cpp
class Solution {
public:
    void rotate_frame(vector<vector<int>> &img,int start, int end){
        for(int i=0 ; start+i <end; i++){
            
            int temp = img[start][start + i];
            img[start][start+i] = img[end-i][start];
            img[end-i][start] = img[end][end -i];
            img[end][end-i] = img[start+i][end];
            img[start+i][end] = temp;
        }
    }
    
    void rotate(vector<vector<int>>& matrix) {
        int size = matrix.size();
        
        for(int layer =0 ; layer<size/2; layer++){
            rotate_frame(matrix,layer,size-layer-1);
        }
    }
};
```

### **Notes**

* Thing of Matrix as frames.
* Try Rotataing frames one by one until you reach middle.
* Just need to figure how elements rotate in frames and accordingly swap.
  