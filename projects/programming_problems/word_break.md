---
layout: post
title: Word Break
subtitle: Sorry its all C++!
bigimg: "img/programming/programming.jpg"
tags: [recursion, backtracking, Leetcode]
---

## **Word Break**<br/>[Leetcode](https://leetcode.com/problems/word-break/)
Given a non-empty string s and a dictionary wordDict containing a list of non-empty words, determine if s can be segmented into a space-separated sequence of one or more dictionary words.

Note:

The same word in the dictionary may be reused multiple times in the segmentation.

```cpp
class Solution {
public:

    bool is_valid(string word, vector<string>& wordDict){
        for(int i=0; i< wordDict.size(); i++){
            if(word == wordDict[i]){
                return true;
            }
        }
        
        return false;
    }
    
    bool word_helper(string &s, int start, vector<string> &wordDict, vector<int> &state){
        if(start == s.length()) return true;
        
        if(state[start] == 1) return false;
        
        for(int i= start; i<s.length(); i++){
            if(is_valid(s.substr(start,i-start+1),wordDict)){
                if(word_helper(s,i+1,wordDict,state)){
                    
                    return true;
                }
                
                else{
                    state[i+1] = 1;
                }
            }
        }
        
        
        return false;
    }
    
    bool wordBreak(string s, vector<string>& wordDict) {
        
        //0 is unvisited
        //1 is word not found
        //-1 is visiting
        
        vector<int> state(s.length(),0);
        return word_helper(s,0,wordDict,state);
        
    }
};
```

### **Notes**

* Recursion Question.
* Bactrack solution, identify base cases, memoize solutions.