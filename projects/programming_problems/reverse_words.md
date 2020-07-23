---
layout: post
title: Rotate Image
subtitle: Sorry its all C++!
bigimg: "img/programming/programming.jpg"
tags: [Array, String, Leetcode]
---

## **Reverse Words in a String** <br/>[Leetcode](https://leetcode.com/problems/reverse-words-in-a-string/)

Given an input string, reverse the string word by word.

    Example 1:

    Input: "the sky is blue"
    Output: "blue is sky the"

```cpp
class Solution {
public:
    string reverseWords(string s) {
        
        if(s.empty()) return s;
        int st = 0;
        while(s[st] == ' '){st++;}
        
        s= s.substr(st,s.length()-st); //Removes spaces from front
        std::reverse(s.begin(),s.end());
        string out;
        
        int word_start = 0;
        while(s[word_start] == ' '){word_start++;}
    
        s = s.substr(word_start, s.length()-word_start);// Remove spaces from back
        
        if(s.empty() || s.length() == 1){
            return s;
        }
        
        int i=0;
        word_start=0;
        while(i < s.length()){
            
            if(s[i]==' ' || i == s.length()-1){
                
                bool is_end = false;
                int last_word_end = i-1;
                
                if(i == s.length()-1){
                    last_word_end = i;
                    is_end =true;
                }
                
                while(s[i] == ' ' && i != s.length()-1){
                    i++;
                }
                //Extract Word
                string word = s.substr(word_start, last_word_end -word_start+1); 
                std::reverse(word.begin(),word.end()); //Reverse
           
                if(!is_end){
                    word += " ";
                }
                out += word ; //append to result
                word_start = i;

                //corner case when a single letter at end
                if(word_start == s.length()-1 && s[word_start -1 ] == ' '){}
                    out+= s[word_start];
                }
               
            }
            
            i++;
        }
        
        return out;
    }
};
```

### **Notes**

* Remove spaces from start.
* Reverse Whole string and again remove spaces.
* Now go through the string keeping track of where last word ended and keep removing spaces.
* Update Start word when you encounter a word after a space.
