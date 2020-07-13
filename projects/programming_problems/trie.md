---
layout: post
title: Trie
subtitle: Sorry its all C++!
bigimg: "img/programming/programming.jpg"
tags: [trie, Leetcode]
---

## **Implement Trie (Prefix Tree)**<br/>[Leetcode](https://leetcode.com/problems/implement-trie-prefix-tree/)

Implement a trie with insert, search, and startsWith methods.

```cpp
class Node{
    
public: 
    unordered_map<char,Node*> n_map;
    bool isWord;
    
    Node(){
        isWord = false;
    }
    
    bool contains(char ch){
        if(n_map.find(ch) != n_map.end()){
            return true;
        }
        
        return false;
    }
    
};


class Trie {
public:
    
    Node* root;
    
    /** Initialize your data structure here. */
    Trie() {
        
        root = new Node();
    }
    
    /** Inserts a word into the trie. */
    void insert(string word) {
        
        Node* curr = root;
        
        for(int i=0 ;i <word.length();i++){
            
            if(!curr->contains(word[i])){
                curr->n_map[word[i]] = new Node();
            }
            
            curr = curr->n_map[word[i]];
            
        }
        curr->isWord = true;
        
    }
    
    /** Returns if the word is in the trie. */
    bool search(string word) {
        Node* curr = root;
        
        for(int i=0 ; i < word.length(); i++){
            if(!curr->contains(word[i])){
                return false;
            }
            
            curr = curr->n_map[word[i]];
        }
        
        return curr->isWord;
    }
    
    /** Returns if there is any word in the trie that starts with the given prefix. */
    bool startsWith(string prefix) {
        Node* curr = root;
        
        for(int i=0 ; i <prefix.length(); i++){

            if(!curr->contains(prefix[i])){
                return false;
            }
            
            curr = curr->n_map[prefix[i]];
        }
        
        return true;
        
    }
};
```