---
layout: post
title: Possible Bipartition
subtitle: Sorry its all C++!
bigimg: "img/programming/programming.jpg"
tags: [graph,bipartition,search]
---

## **Finding Groups in Bipartite Graphs**<br/> [LeetCode](https://leetcode.com/problems/possible-bipartition/)

Given a set of N people (numbered 1, 2, ..., N), we would like to split everyone into two groups of any size.

Each person may dislike some other people, and they should not go into the same group. 

Formally, if dislikes[i] = [a, b], it means it is not allowed to put the people numbered a and b into the same group.

Return true if and only if it is possible to split everyone into two groups in this way.

```cpp
class Solution {
public:
    bool possibleBipartition(int N, vector<vector<int>>& dislikes) {
        vector<int> stat(N,0);
        vector<vector<int>> graph(N);

        for(auto dislike:dislikes)
        {
            graph[dislike[0]-1].push_back(dislike[1]-1);  //creating an undirected graph

            graph[dislike[1]-1].push_back(dislike[0]-1);

        }

        vector<int> group1;
        vector<int> group2;
        for(int i =0; i<N; i++)
        {
            if(stat[i] == 1) continue;

            vector<int> levels(N,-1);
            int start = i;
            levels[start] = 0;
            queue<int> bfs_q;
            bfs_q.push(start);
            stat[start] = -1;
            int curr_level = 0;
            while(!bfs_q.empty())
            {
                int curr_node = bfs_q.front();
                bfs_q.pop();

                if(stat[curr_node] == 1) continue;

                curr_level = levels[curr_node] + 1;
                if(curr_level%2 == 0) //adding to corresponding group
                {
                    group1.push_back(curr_node);
                }
                else
                {
                    group2.push_back(curr_node);
                }
                for(int ngb: graph[curr_node])
                {
                    if(stat[ngb] == 1) continue;
                    if(levels[ngb] == levels[curr_node]) return 0;
                    bfs_q.push(ngb);
                    stat[ngb] = -1;
                    levels[ngb] = curr_level;
                }
                stat[curr_node] = 1;
            }

        }
        for(auto a:group1){
            cout<<a+1<<" ";
        }
        return 1;
    }
};
```

### **NOTES**

* Maintain the expansion level during bfs.
* All nodeat even levels go to one class and the odd ones go to the other
* given the edges only convert it to a graph first.