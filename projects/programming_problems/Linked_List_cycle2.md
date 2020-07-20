---
layout: post
title: Linked List Cycle 2
subtitle: Sorry its all C++!
bigimg: "img/programming/programming.jpg"
tags: [Linked List, Leetcode]
---
# **Linked List Cycle 2**<br/>[Leetcode](https://leetcode.com/problems/linked-list-cycle-ii/)
Given a linked list, return the node where the cycle begins. If there is no cycle, return null.

To represent a cycle in the given linked list, we use an integer pos which represents the position (0-indexed) in the linked list where tail connects to. If pos is -1, then there is no cycle in the linked list.

Note: Do not modify the linked list.

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        
        ListNode* fast = head;
        ListNode* slow = head;
        
        while(fast != NULL){
            fast = fast->next;
            
            if(fast == slow){
                break;
            }
            if(fast != NULL){
                fast = fast->next;
                
                if(fast == slow){
                    break;
                }
            }
            slow = slow->next;
        }
        if(fast == NULL){
            return NULL;
        }
        fast = fast->next;
        int length = 1;

        while(fast != slow){
            fast = fast->next;
            length++;
        }
        ListNode* start = head;
        ListNode* end = head;
        
        for(int i=0; i<length; i++){
            start = start->next;
        }
        
        while(start!= end){
            start = start->next;
            end = end->next;
        }
        
        return end;
    }
};
```
### **Notes**

* Use Fast Slow pointer technique.
* Find Length of the cycle.
* Start two pointers, move one equal to length of the cycle, start moving other until they meet.
