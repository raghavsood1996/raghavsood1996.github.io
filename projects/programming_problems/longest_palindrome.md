---
layout: post
title: Longest Palindromic Substring
subtitle: Sorry its all C++!
bigimg: "img/programming/programming.jpg"
tags: [Array, String, Sliding Window, Leetcode]
---

## **Longest Palindromic Substring**<br/>[Leetcode](https://leetcode.com/problems/longest-palindromic-substring/)

Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.

    Example 1:

    Input: "babad"
    Output: "bab"
    Note: "aba" is also a valid answer.

```cpp
class Solution {
public:
    string longestPalindrome(string s) {
        if(s.empty()){
            return s;
        }
        //taking care of odd palindromes
        int m_start = 0;
        int m_end  = 0;
        int longest = 1;
        
        for(int i = 0; i<s.length(); i++){
            
            int offset = 0;
            while(i-1-offset >= 0 && i+1+offset < s.length() && s[i-1-offset] == s[i+1+offset]){
               offset++;
            }
            
            int length = 2*offset+1;
            if(length > longest){
                longest = length;
                m_start = i-offset;
                m_end = i+offset;
            }
        }
        
        //even palindromes
        for(int i=0; i<s.length();i++){
            int offset = 0;
            
            while(i-offset >=0 && i+offset+1 < s.length() && s[i-offset] == s[i+offset+1]){
                offset++;
            }
            
            int length = 2*offset;
            
            if(length > longest){
                longest = length;
                m_start = i-offset+1;
                m_end = i+offset;
                
            }
        }
        
        return s.substr(m_start,m_end-m_start+1);
    }
};
```

### **Notes**

* Take care of odd and even palindromes.
* Use sliding window technique to look for longest palindromic substring.