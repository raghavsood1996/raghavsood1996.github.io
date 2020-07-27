---
layout: post
title: Coin Change 2
subtitle: Sorry its all C++!
bigimg: "img/programming/programming.jpg"
tags: [Recursion, Dynamic Programming,Leetcode]
---

## **Coin Change 2**<br/>[Leetcode](https://leetcode.com/problems/coin-change-2/)

You are given coins of different denominations and a total amount of money. Write a function to compute the number of combinations that make up that amount. You may assume that you have infinite number of each kind of coin.

```cpp
class Solution {
public:
    
    int change(int amount, vector<int>& coins) {
        
        vector<int> res(amount+1,0);
        res[0] = 1;
        
        for(auto &coin:coins){
            
            for(int j = coin ; j<= amount; j++){
                
                res[j] =  res[j] + res[j-coin] ; // reccurence relation
            }
        }
        return res[amount];
    }
};
```

### **Notes**

* Dynamic Programming Question
* Easier to think about in tabular form but can also think recursively. 
