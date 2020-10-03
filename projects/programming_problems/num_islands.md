---
layout: post
title: Number of Islands
subtitle: Sorry its all C++!
bigimg: "img/programming/programming.jpg"
tags: [graph,connected components,search]
---

## **Number of Islands**<br/>[Leetcode](https://leetcode.com/problems/number-of-islands/)

Given a 2d grid map of '1's (land) and '0's (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

```cpp
class Solution {
public:
    char query(int y, int x, vector<vector<char>>& grid) //helper funtion for reading the grid
    {
        int rows = grid.size();

        int cols = grid[0].size();
        if(y >= rows || y<0 || x>=cols || x<0){
            return '0';
        }

        else{
            return grid[y][x];
        }

    }

    int numIslands(vector<vector<char>>& grid) {
        int rows = grid.size();
        if(rows == 0) return 0;
        int cols = grid[0].size();
        vector<vector<int> > visited(rows,vector<int>(cols,0)); //maintaing the status of the nodes

        int n_dx[4] = {1,0,-1,0}; //4 connected grid neighbors
        int n_dy[4] = {0,1,0,-1};

        int num_islands = 0;

        for(int i=0; i<rows; i++){
            for(int j=0; j<cols; j++){
                if(grid[i][j] == '0' || visited[i][j] == 1) continue;
                num_islands++ ;

                char start = grid[i][j];
                queue<pair<int,int>> bfs_q; //using std pair for storing pair of coordinates
                bfs_q.push(make_pair(i,j));
                visited[i][j] = -1;

                while(!bfs_q.empty()){
                    auto curr = bfs_q.front();
                    bfs_q.pop();
                    if(visited[curr.first][curr.second] == 1) continue;

                    for(int n=0;n<4; n++)
                    {
                        int n_y= curr.first + n_dy[n];
                        int n_x = curr.second +n_dx[n];
                        if(query(n_y,n_x,grid) == '1' && visited[n_y][n_x] == 0) //if neighbor is land and not visited keep going
                        {
                            bfs_q.push(make_pair(n_y,n_x));
                            visited[n_y][n_x] = -1;
                        }

                        visited[curr.first][curr.second] = 1;
                    }
                }
            }
        }
        return num_islands;
    }
};
```