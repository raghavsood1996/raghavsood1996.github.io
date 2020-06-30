---
layout: post
title: Longest Substring Without Repeating Characters
subtitle: Sorry its all C++!
bigimg: "img/programming/programming.jpg"
tags: [array, subarray, sliding_winodw, Leetcode]
---

## **Longest Substring Without Repeating Characters** <br/> [Leetcode](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

Given a string, find the length of the longest substring without repeating characters. 

```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {

        if(s.empty()){
            return 0;
        }
        int start = 0;
        int end = 0;
        int max_length =1;
        map<char,int> c_map;

        c_map[s[start]] = start;

        while(end < s.length() -1){
            end ++;

            char to_add = s[end];

            if(c_map.find(to_add) != c_map.end() && c_map[to_add] >= start){
                start = c_map[to_add] + 1;
                c_map[to_add] = end;
            }

            else{

                c_map[to_add] = end;
            }

            int len = end-start +1 ;

            if(len > max_length){
                max_length = len;
            }
        }

        return max_length;

    }
```

### **Notes**

* Subarray problem solved using sliding window technique.
  