---
layout: post
title: DFS Graph
subtitle: Sorry its all C++!
bigimg: "img/programming/programming.jpg"
tags: [graph,search]
---

## **DFS GRAPH**

```c++
#include <iostream>
#include <list>
#include<memory>
using namespace std;

class Node{
    public:
    int val;
    int stat; //0 if unvisited 1 if visited and -1 if visiting
    list<Node*> neighbors;

    Node(int val){
        this->val = val;
        this->stat = 0;
    }
};

class Graph{
    public:
    list<Node*> vertices;
};

bool dfs_visit(Node* n,int target){
    if(n->stat == 1){
        return 0;
    }
    if(n->val == target){

        return 1;
    }

    n->stat = -1; //visiting
    for(auto neigh: n->neighbors){
        if(dfs_visit(neigh,target)){
            return 1;
        };
    }

    n->stat = 1; //visited
    return 0;

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

    if(dfs_visit(&n1,target)){
        cout<<"target found";
    }
    else{
        cout<<"not found"<<"\n";
    }

    return 0;
};
```