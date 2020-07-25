---
layout: post
title: Course Schedule 2
subtitle: Sorry its all C++!
bigimg: "img/programming/programming.jpg"
tags: [Graph, DFS, Topology Sort, Leetcode]
---

## **Course Schedule 2**<br/>[Leetcode](https://leetcode.com/problems/course-schedule-ii/)

There are a total of n courses you have to take, labeled from 0 to n-1.

Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: [0,1]

Given the total number of courses and a list of prerequisite pairs, return the ordering of courses you should take to finish all courses.

There may be multiple correct orders, you just need to return one of them. If it is impossible to finish all courses, return an empty array.

```cpp
class Solution {
public:
    
    bool dfs_visit(int &node, vector<int> &node_stat, vector<vector<int>> &adj_list, stack<int> &top_sort){
        
        if(node_stat[node] == 1){
            return 1; //if already visited
        }
        
        if(node_stat[node] == -1){
            return 0; //if visiting 
        }
        
        node_stat[node] = -1; //mark visiting
        
        for(int ngb : adj_list[node]){
            
            if(!dfs_visit(ngb, node_stat, adj_list, top_sort)){
                return 0;
            }
        }
        
        node_stat[node] = 1; //visited
        top_sort.push(node); //push in the stack
        
        return 1;
    }
    
    vector<int> findOrder(int numCourses, vector<vector<int>>& prerequisites) {
        
        vector<vector<int>> adj_list(numCourses);
        
        for(auto pair: prerequisites){ //Create an adjacency List
            adj_list[pair[1]].push_back(pair[0]);
        }
        
        vector<int> node_stat(numCourses,0); //maintain status for each node
        stack<int> top_sort;
        vector<int> order;
        
        for(int i=0 ; i<numCourses; i++){ //visit all nodes
            if(node_stat[i] == 0){
                if(!dfs_visit(i,node_stat,adj_list,top_sort)){
                    return order;
                }
            }
        }
        
        //topological sorted graph gives the order
        while(!top_sort.empty()){
            
            int temp = top_sort.top();
            top_sort.pop();
            order.push_back(temp);
        }
        
        return order;
    }
};
```

### **Notes**

* Simple question of DFS with stack for topological sort.
* If there is a cycle in a graph then the problem has no solution.