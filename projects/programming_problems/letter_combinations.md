---
layout: post
title: Letter Combinations of a Phone Number
subtitle: Sorry its all C++!
bigimg: "img/programming/programming.jpg"
tags: [recursion, buffer, Leetcode]
---

## **Letter Combinations of a Phone Number**<br/>[Leetcode](https://leetcode.com/problems/letter-combinations-of-a-phone-number/)

Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent.

A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

```cpp
class Solution {
public:
    
    vector<string> combs;
    unordered_map<char,vector<char>> letter_map;
    
    void init_letter_map(){
        
        letter_map['2'] = {'a','b','c'};
        letter_map['3'] = {'d','e','f'};
        letter_map['4'] = {'g','h','i'};
        letter_map['5'] = {'j','k','l'};
        letter_map['6'] = {'m','n','o'};
        letter_map['7'] = {'p','q','r','s'};
        letter_map['8'] = {'t','u','v'};
        letter_map['9'] = {'w','x','y','z'};
        
        return ;
    }
    
    void add_comb(char buffer[],int buffer_idx){
        
        string comb ="";
        for(int i =0 ;i < buffer_idx; i++){
            comb += buffer[i];
        }
        combs.push_back(comb);
    }
    
    void all_combs(string &digits, char buffer[], int buff_idx, int start_idx){

        //if buffer is full add it 
        if(buff_idx >= digits.length() || start_idx >= digits.length()){
            add_comb(buffer,buff_idx);
            return;
        }

        auto letters = letter_map[digits[start_idx]];
        
        //go through letter possibilities for a digit
        for(auto letter: letters){

            buffer[start_idx] = letter;
            all_combs(digits, buffer, buff_idx+1, start_idx+1);
        }
        
        return;
    }
    
    vector<string> letterCombinations(string digits) {

        if(digits.empty()){
            return combs;
        }
        init_letter_map();
        char buffer[digits.length()];
        all_combs(digits,buffer,0,0);
        
        return combs;
        
    }
};
```

### **Notes**

* Recursion Question.
* Maintain a buffer and keep filling in a recursive way.
* Once the buffer is full add it and backtrack.
