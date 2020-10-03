---
layout: post
title: BFS Graph
subtitle: Sorry its all C++!
bigimg: "img/programming/programming.jpg"
tags: [graph,search]
---

## **BFS GRAPH**

```cpp
#include <iostream>
#include <list>
#include<memory>
#include<queue>
using namespace std;

class Node
{
    public:
    int val;
    int stat; //0 if unvisited 1 if visited and -1 if visiting
    list<Node*> neighbors;

    Node(int val){
        this->val = val;
        this->stat = 0;
    }
};

class Graph
{
    public:
    list<Node*> vertices;
};

void bfs(Node* start)
{
    if(start->stat == 1|| start== NULL)
    {
        return;
    }

    queue<Node*> q;
    q.push(start);
    start->stat = -1;
    while(!q.empty())
    {
        Node* current = q.front();
        q.pop();

        std::cout<<current->val<<"\n"; //processing the current node
        for(auto neigh: current->neighbors)
        {
            if(neigh->stat == 0) //only processing the unvisited nodes
            {
                q.push(neigh);
                neigh->stat = -1;
            }
        }
        current->stat = 1;
    }
    return;
}

int main()
{

    Node n1(1),n2(5),n3(6),n4(8),n5(7),n6(9);
    Graph le_graph;
    n1.neighbors.push_back(&n2);
    n1.neighbors.push_back(&n3);
    n2.neighbors.push_back(&n4);
    n3.neighbors.push_back(&n4);
    n3.neighbors.push_back(&n5);
    n4.neighbors.push_back(&n6);

    le_graph.vertices.push_back(&n1);
    le_graph.vertices.push_back(&n2);
    le_graph.vertices.push_back(&n3);
    le_graph.vertices.push_back(&n4);
    le_graph.vertices.push_back(&n5);
    le_graph.vertices.push_back(&n6);
    int target = 100;


    bfs(&n1);

    return 0;
    }
```
