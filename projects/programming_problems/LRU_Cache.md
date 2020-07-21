---
layout: post
title: LRU Cache
subtitle: Sorry its all C++!
bigimg: "img/programming/programming.jpg"
tags: [Linked List, Hash Table, Leetcode]
---

## **LRU Cache**<br/>[Leetcode](https://leetcode.com/problems/lru-cache/)

Design and implement a data structure for Least Recently Used (LRU) cache. It should support the following operations: get and put.

get(key) - Get the value (will always be positive) of the key if the key exists in the cache, otherwise return -1.
put(key, value) - Set or insert the value if the key is not already present. When the cache reached its capacity, it should invalidate the least recently used item before inserting a new item.

The cache is initialized with a positive capacity.

```cpp
struct Node{
    int val;
    int key;
    Node* next;
    Node* prev;
    
    Node(int val ,int key){
        this->val =  val;
        this->next = NULL;
        this->prev = NULL;
        this->key = key;
    }
};

class LRUCache {
public:
    Node* head;
    Node* tail;
    int capacity;
    int curr_size;
    unordered_map<int,Node*> cache_map;
    
    LRUCache(int capacity) {
        this->capacity = capacity;
        this->head = NULL;
        this->tail = NULL;
        this->curr_size = 0;
        
    }
    
    int get(int key) {
        //key not found
        if(cache_map.find(key) == cache_map.end()){
            return -1;
        }
        
        auto ret = cache_map[key];
        auto value = ret->val;
        //if key found erase it from current pos and put it in front
        cache_map.erase(key);
        ListRemove(ret);
        ListAdd(key,value);
        
        return value;

    }

    void put(int key, int value) {
        //if key is already there just delete older vesrion and 
        // add newer version
        if(cache_map.find(key) != cache_map.end()){
            cache_map[key]->val = value;
            ListRemove(cache_map[key]);
            cache_map.erase(key);
            ListAdd(key,value);
            return;
        }
        
        //if cache map is full , earse the key at back and insert new
        if(cache_map.size() == capacity){
            cache_map.erase(head->key);
            ListRemove(head);
        }
        ListAdd(key,value);
    }

    void ListRemove(Node* nd){
        
        if(nd->prev != NULL) nd->prev->next = nd->next;
        if(nd->next != NULL) nd->next->prev = nd->prev;
        
        if(nd == head){
            head = nd->next;
        }
        
        if(nd == tail){
            tail = nd->prev;
        }
    
        return;
    }
    
    void ListAdd(int key, int val){

        Node* tmp = new Node(val,key);
        if(head == NULL){
            head = tmp;
            tail = tmp;
            cache_map.emplace(key,tmp);
            return;
        }
        
        tail->next = tmp;
        tmp->prev = tail;
        tail = tmp;
        cache_map.emplace(key,tmp);

        return;
    }
};

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache* obj = new LRUCache(capacity);
 * int param_1 = obj->get(key);
 * obj->put(key,value);
 */
 ```

### **Notes**

 * Use a linked hash table to store pointer to store pointer to each node in the linked list.
 * 0(1) lookup for all elements.
 * Place ercently used element in front of the list.
 * When capacity is full delete the elment at the back and insert new at front.