---
layout: page
title: LeetCode Madness
subtitle: Sorry its all C++!
bigimg: "img/programming/programming.jpg"
---

## **Search in rotated array** <br/>[Leetcode](https://leetcode.com/problems/search-in-rotated-sorted-array/)

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.
(i.e., $[0,1,2,4,5,6,7]$ might become $[4,5,6,7,0,1,2]$).

You are given a target value to search. If found in the array return its index, otherwise return -1.

You may assume no duplicate exists in the array.

Your algorithm's runtime complexity must be in the order of O(log n).

**Example 1:**
**Input**: $\mathbf{nums = [4,5,6,7,0,1,2]}$, **target** = 0.
**Output**: 4 <br/>

**Example 2:**
**Input:** $\mathbf{nums = [4,5,6,7,0,1,2]}$, **target** = 3 **Output:** -1

```cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int start = 0, end = nums.size()-1;
        while(start <= end){
            cout<<start<<" "<<end<<endl;
            int mid = (start + end)/2;
            if(target == nums[mid]){
                return mid;
            }
            else if(nums[mid] >= nums[start]){ //unrotated part of the array
                if(target >= nums[start] && target < nums[mid]) 
                    end = mid-1;
                else
                    start = mid+1;
            }
            else{ //rotated part of the array
                if(target <= nums[end] && target > nums[mid])
                    start = mid+1;
                else
                    end = mid-1;
            }
        }
        cout<<start<<" "<<end<<endl;
        return -1;
    }
};
```

### **Notes**

* Binary Search Problem
* Figure out what part of the array the middle element and target belong to and accordingly change start and end of the binary search.

## **Validating a BST** <br/> [Leetcode](https://leetcode.com/problems/validate-binary-search-tree/submissions/)

```c++
/**
* Definition for a binary tree node.
* struct TreeNode {
*     int val;
*     TreeNode *left;
*     TreeNode *right;
*     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
* };
*/
class Solution {
public:

    pair<long,long>* bst_util(TreeNode* node){
        if(node == NULL){
            pair<long,long>* max_min = new pair<long,long>;
            *max_min = make_pair(LONG_MIN,LONG_MAX);
            return max_min;
        }


        auto left_max_min = bst_util(node->left);
        auto right_max_min = bst_util(node->right);

        if(left_max_min == NULL || right_max_min == NULL){
            return NULL;
        }


        if(left_max_min->first >= node->val || right_max_min->second <= node->val){
            return NULL;
        }


        long l_max = node->left == NULL ? node->val : left_max_min->second; //returning min val of right subtree
        long r_min = node->right == NULL ? node->val : right_max_min->first; //returning max value of left subtree

        pair<long,long>* ret = new pair<long,long>;

        *ret = make_pair(r_min,l_max);
        return ret;

    }


    bool isValidBST(TreeNode* root) {

        if(root == NULL || (root->left == NULL && root->right == NULL)){
            return 1;
        }

        if(bst_util(root))
        {
            return true;
        }

        return false;
    }
};
```

### **Notes**

* Make sure the Maximum of the left subtree is less than the root and min orf the right subtree is greater than the root.
* Do it in bottom to top fashion considering the leave nodes as always balanced.

## **Coin Change Problem DP**<br/> [Leetcode](https://leetcode.com/problems/coin-change/)

You are given coins of different denominations and a total amount of money amount. Write a function to compute the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return -1.

```c++
class Solution {
public:

    int util_coins(vector<int>& coins, int amount ,vector<int> &count){

        if(amount == 0){
            return 0;
        }

        if(amount< 0){
            return -1;
        }

        if(count[amount-1] != 0) return count[amount-1];

        int min = INT_MAX;
        for(int coin:coins){
            int res = util_coins(coins,amount- coin,count) ;
            if(res>=0 && res <min){
                min = 1 + res;
            }
        }
        count[amount-1] = min == INT_MAX ? -1 :min;

        return count[amount-1];
    }

    int coinChange(vector<int>& coins, int amount) {
    if(amount < 1){
        return 0;
    }
        vector<int> count(amount+1,0);
        return util_coins(coins,amount,count);
    }
};
```

### **Intution**

We can use top to bottom approach of Dynamic Programming. Optimal substructure of the problem is <br/>$F(s) = F(s-c) +1$ .<br/> But as we dont know the denomination of the closest last coin C to S. We compute $F(S-C_i)$ for each possible denomination and choose the minimum among them.  The following recuurence relation holds:<br/>
$F(S) = \min_{i=0..n-1} F(S-c_i)+1$ <br/>
subject to $S-c_i \geq 0$.

## **Lowest Common Ancestor BST**<br/>[Leetcode](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/submissions/)

```c++
    /**
* Definition for a binary tree node.
* struct TreeNode {
*     int val;
*     TreeNode *left;
*     TreeNode *right;
*     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
* };
*/
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if(root == NULL){
            return NULL;
        }

        //keep going left or right until both p and q are on different sides of the tree
        if(root->val < p->val && root->val <q->val){
            return(lowestCommonAncestor(root->right,p,q));
        }

        if(root->val >p->val && root->val > q->val){
            return (lowestCommonAncestor(root->left,p,q));
        }


        else{
            return root;
        }
    }
};
```

## **Merge Intervals**<br/> [Leetcode](https://leetcode.com/problems/merge-intervals/)

Given a collection of intervals, merge all overlapping intervals.

```c++
struct Point{
int val;
bool start;


Point(int val,bool start){
    this->val = val;
    this->start = start;
}


};

struct less_than_key{ //custom comparator
    inline bool operator()(const Point &p1, const Point &p2){
        if(p1.val == p2.val){
            if(p1.start){
                return 1;
            }
        }
        return (p1.val < p2.val);
    }

};


class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {

        vector<Point> points;
        for(auto interval : intervals){
            Point start(interval[0],1);
            points.push_back(start);
            Point end(interval[1],0);
            points.push_back(end);
        }


        sort(points.begin(),points.end(),less_than_key());
        vector<vector<int>> merged_intervals;

        int start;
        int num_intervals = 0;
        for(int i=0; i<points.size();i++){
            if(points[i].start){
                num_intervals++;
                if(num_intervals == 1){
                    start = points[i].val;
                }
            }

            else if(!points[i].start){
                num_intervals--;
                if(num_intervals == 0){
                    vector<int> m_int(2);
                    m_int[0] = start;
                    m_int[1] = points[i].val;
                    merged_intervals.push_back(m_int);
                }
            }
        }


        return merged_intervals;
    }
};
```

### **Notes**

* Line Sweep Algorithm
* Have a custom class point with start and end ids.
* sort the vector of points according to time vals.
* go through the vector and accordingly modify the count and keep track of start and end of overlapping intervals.

## **Kth order Statistics (Selection Algorithm)**<br/>[Leetcode](https://leetcode.com/problems/kth-largest-element-in-an-array/submissions/)

Find the kth largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.

```c++
    class Solution {
    public:

    int get_random( int start, int end){
        if (start > end){
            cout<<"ERROR"<<"\n";
        }
        int randNum = rand()%(end-start + 1) + start;
        return randNum;
    }

    int partition(vector<int> &nums, int pivot_idx, int start, int end){
        int less = start;
        for(int i = start + 1; i<= end; i++){
            if(nums[i] <= nums[start]){
                swap(nums[i],nums[++less]);
            }
        }

        swap(nums[start],nums[less]);
        return less;
    }

    int findkthUtil(vector<int>& nums, int tar_idx, int start,int end){

        int rand_idx = get_random(start,end);
        int pivot_idx = partition(nums,pivot_idx,start,end);

        if(pivot_idx == tar_idx){
            return nums[pivot_idx];
        }

        else if(pivot_idx > tar_idx){
            return findkthUtil(nums,tar_idx,start,pivot_idx - 1);
        }

        else{
            return findkthUtil(nums,tar_idx,pivot_idx+1,end);
        }
    }

    int findKthLargest(vector<int>& nums, int k) {
        int start =0;
        int end = nums.size()-1;
        srand(time(NULL));
        return findkthUtil(nums,nums.size() - k,start,end);
    }
};
```
### **Notes**

* Algorithm for finding kth smallest or largest element in array.
* The Average expected time is $O(n)$ and he worst case time is $O(n^2)$.

## **Merge Sort**

```c++
    class Solution {
    public:

        void merge(vector<int>& nums,int start, int mid,int end){
            int itr1= start;
            int itr2= mid+1;

            vector<int> merged;
            while(itr1 <= mid && itr2 <= end){

                if(nums[itr1] <= nums[itr2]){
                    merged.push_back(nums[itr1]);
                    itr1++;
                }
                else{
                    merged.push_back(nums[itr2]);
                    itr2++;
                }
            }

            while(itr1<=mid){
                merged.push_back(nums[itr1]);
                itr1++;
            }

            while(itr2<= end){
                merged.push_back(nums[itr2]);
                itr2++;
            }

            int itr =0 ;

            for(int i = start; i<= end; i++){
                nums[i] = merged[itr];
                itr++;
            }
        }

        void merge_sort(vector<int> &nums, int start,int end){
            if(start >= end){
                return;
            }

            int mid = start + (end-start)/2;
            merge_sort(nums,start,mid);
            merge_sort(nums,mid+1,end);
            merge(nums,start,mid,end);
        }
        vector<int> sortArray(vector<int>& nums) {

            int start = 0;
            int end = nums.size()-1;
            merge_sort(nums,start,end);
            return nums;

        }
    };
```

## **Distribute Coins in a Binary Tree**<br/>[Leetcode](https://leetcode.com/problems/distribute-coins-in-binary-tree/solution/)
Given the root of a binary tree with N nodes, each node in the tree has node.val coins, and there are N coins total.

In one move, we may choose two adjacent nodes and move one coin from one node to another.  (The move may be from parent to child, or from child to parent.)

Return the number of moves required to make every node have exactly one coin.

```c++
    class Solution {
        public:
            int ans;
            int distributeCoins(TreeNode* root) {
                ans = 0;
                dfs(root);
                return ans;
            }

            int dfs(TreeNode* node) {
                if (node == NULL) return 0;
                int L = dfs(node->left);
                int R = dfs(node->right);
                ans += abs(L) + abs(R);
                return node->val + L + R - 1;
            }
};
```

### **NOTES**

* **Intiution**: Moves to baalnce a leaf is $abs(NumCoins_{leaf} -1)$
* **Algorithm**: &nbsp; $moves_{node} = moves_{left} + moves_{right} + node\rightarrow val -1$

## **Binary Tree Pruning**<br/>[Leetcode](https://leetcode.com/problems/binary-tree-pruning/)

We are given the head node root of a binary tree, where additionally every node's value is either a 0 or a 1. Return the same tree where every subtree (of the given tree) not containing a 1 has been removed.

```c++
class Solution {
    public:
        bool prune_helper(TreeNode* node, TreeNode* parent){
            if(node == NULL){

                if(parent->val == 1){
                    return 1;
                }
                else{
                    return 0;
                }
            }

            bool left = prune_helper(node->left,node);
            bool right = prune_helper(node->right,node);

            if(!left) node->left = NULL;
            if(!right) node->right = NULL;

            if(!left && !right && node->val != 1 ){
                return 0;
            }

            return 1;
        }

        TreeNode* pruneTree(TreeNode* root) {

            bool var = prune_helper(root, NULL);
            return root;
        }
};
```

## **Notes**

* Recursively from bottom to top check subtrees and make pointers NULL accordingly.

## **Finding Duplicate Subtrees**<br/>[Leetcode](https://leetcode.com/problems/find-duplicate-subtrees/)

Given a binary tree, return all duplicate subtrees. For each kind of duplicate subtrees, you only need to return the root node of any one of them.

### **Approach 1**

```c++
    class Solution {
    public:

    int height_map(TreeNode* node,map<int,vector<TreeNode*>> &h_map){
        if(node == NULL){
            return -1;
        }

        int height = max(height_map(node->left,h_map),height_map(node->right,h_map)) +1;

        h_map[height].push_back(node);

        return height;
    }

    // compare two subtrees
    bool compare_trees( TreeNode* root_a, TreeNode* root_b){
        if(root_a == NULL && root_b == NULL){
            return true;
        }

        if(root_a == NULL || root_b == NULL){
            return false;
        }

        if(root_a->val != root_b->val){
            return false;
        }

        else{
            return (compare_trees(root_a->left,root_b->left) && compare_trees(root_a->right,root_b->right));
        }
    }

    //compare all subtrees at the same height
    vector<TreeNode*> findDuplicateSubtrees(TreeNode* root) {
        map<int,vector<TreeNode*>> h_map;
        int ht = height_map(root, h_map);
        vector<TreeNode*> duplicates;

        map<int, vector<TreeNode*>>::iterator it;
        for(it = h_map.begin(); it != h_map.end(); it++){
            vector<TreeNode*> same_height = it->second;
            vector<bool> visited(same_height.size(),0);

            for(int i =0; i <same_height.size(); i++){
                int h_count = 0;
                if(visited[i]) continue;
                visited[i] = 1;

                for(int j= i+1; j< same_height.size();j++){
                    if(visited[j]) continue;

                    if(compare_trees(same_height[i],same_height[j])){
                        visited[j] = 1;
                        h_count++;
                        if(h_count == 1){
                            duplicates.push_back(same_height[j]);
                        }
                    }
                }
            }
        }

        return duplicates;
    }
};
```

## **Convert Binary Search Tree to Greater Tree** <br/> [Leetcode](https://leetcode.com/problems/convert-bst-to-greater-tree/submissions/)

Given a Binary Search Tree (BST), convert it to a Greater Tree such that every key of the original BST is changed to the original key plus sum of all keys greater than the original key in BST.

```c++
class Solution {
    public:

        void bst_util(TreeNode* node, int &sum){
            if( node == NULL){
                return ;
            }

            bst_util(node->right,node,0);
            sum += node->val;
            node->val = sum;
            bst_util(node->left,sum);

            return;
        }

        TreeNode* convertBST(TreeNode* root) {

            int sum = 0;
            bst_util(root,sum);
            return sum;
        }
};
```

### **Notes**

* Just do a reverse in order traversal by traversing right subtrees first.
* Maintain a global sum variable and accordingly modify the value of the node.

## **Convert Sorted List to Binary Search Tree** <br/> [Leetcode](https://leetcode.com/problems/convert-sorted-list-to-binary-search-tree/)

Given a singly linked list where elements are sorted in ascending order, convert it to a height balanced BST.

```c++
    class Solution {
    public:

    //Find Median of Linked List using fast and slow pointers
    ListNode* find_median(ListNode* head){
        if(head == NULL){
            return NULL;
        }

        ListNode* slow = head;
        ListNode* fast = head;
        ListNode* prev = NULL;

        while(fast != NULL){
            fast = fast->next;

            if(fast){
                fast = fast->next;
                prev = slow;
                slow = slow->next;
            }
        }

        if(prev) prev->next = NULL;

        return slow;

    }

    TreeNode* bst_util(ListNode* head){

        if(head == NULL){
            return NULL;
        }

        ListNode* mid = find_median(head);
        TreeNode* root = new TreeNode(mid->val);

        if(head == mid){
            return root;
        }

        root->left = bst_util(head);

        root->right = bst_util(mid->next);


        return root;

    }

    TreeNode* sortedListToBST(ListNode* head) {

        return bst_util(head);
    }
};
```

### **Notes**

* Use fast slow pointers to find median of the list.
* Recursively keep splitting the list in two and modify the left and right pointers.

## **Unique Binary Search Trees**<br/>[Leetcode](https://leetcode.com/problems/unique-binary-search-trees/)

Given n, how many structurally unique BST's (binary search trees) that store values 1 ... n?

```c++
class Solution {
public:

    int trees_dp(int n){

        vector<int> map(n+1,0);
        map[0] = 1;
        map[1] = 1;

        for(int i=2 ;i<=n ;i++){
            for(int j=0; j<i ;j++){
                map[i] += map[j]*map[i-j-1];
            }
        }

        return map[n];
    }


    int numTrees(int n) {

        return trees_dp(n);

    }
};
```

### **Notes**

* All nodes in the left subtree are smaller than the root and all nodes in the right subtree are greater than the root.
* If we have ith number as root then the left subtree can have $i-1$

## **Friend Circles**<br/>[Leetcode](https://leetcode.com/problems/friend-circles/)

There are N students in a class. Some of them are friends, while some are not. Their friendship is transitive in nature. For example, if A is a direct friend of B, and B is a direct friend of C, then A is an indirect friend of C. And we defined a friend circle is a group of students who are direct or indirect friends.

Given a N*N matrix M representing the friend relationship between students in the class. If $M[i][j] = 1$, then the ith and jth students are direct friends with each other, otherwise not. And you have to output the total number of friend circles among all the students.

```c++
class Solution {
public:
    void dfs_visit(int person, vector<bool> &visited, vector<vector<int>>& M){

        for(int j = 0; j<M[person].size() ; j++){

            if(visited[j]) continue; //if a person has been visited than skip

            if(M[person][j] == 1){//if friend than visit
                visited[j] = true;
                dfs_visit(j,visited,M);
            }
        }
    }

    int findCircleNum(vector<vector<int>>& M) {
        int groups = 0;
        vector<bool> visited(M.size(),false);

        for(int i=0; i< M.size(); i++){
            if(visited[i]) continue;
            visited[i] = true;
            groups ++;
            dfs_visit(i,visited,M); //visit all the disconnected groups
        }

        return groups;
    }
};
```

### **Notes**

* This a question regarding finding components in a graph
* You try to visit each group using dfs and keep track using a visited flag.
* Very similar to counting islands question.

## **Add Two Numbers**<br/>[Leetcode](https://leetcode.com/problems/add-two-numbers/)

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

```c++
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        auto q1 = l1;
        auto q2 = l2;
        ListNode* curr = new ListNode(0);
        ListNode* ret = curr;
        int carry = 0;
        //Add Two Numbers Like you would manually add them
        while(q1 != NULL || q2 != NULL){
            int num_1 = (q1 == NULL) ? 0 : q1->val;
            int num_2 = (q2 == NULL) ? 0 : q2->val;
            int sum = num_1 + num_2 +carry;
            carry = sum/10;
            curr->next = new ListNode(sum%10);
            curr = curr->next;
            if(q1 != NULL) q1 = q1->next;
            if(q2 != NULL) q2 = q2->next;
        }
        if(carry > 0){
            curr->next = new ListNode(carry);
        }

        return ret->next;
    }
};
```

### **Notes**

* This is a simple linked list question.
* Add numbers like you manually add them using carry system.

## **3Sum Closest**<br/>[Leetcode](https://leetcode.com/problems/3sum-closest/)

Given an array nums of n integers and an integer target, find three integers in nums such that the sum is closest to target. Return the sum of the three integers. You may assume that each input would have exactly one solution.

**Example 1:**

>**Input**: nums = [-1,2,1,-4], target = 1 <br/>
>**Output**: 2 <br/>
>**Explanation**: The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).

```c++
class Solution {
public:

    int threeSumClosest(vector<int>& nums, int target) {

        std::sort(nums.begin(), nums.end());
        int diff = INT_MAX;


        for(int i=0; i<nums.size(); i++){
            int low = i+1;
            int high = nums.size()-1;

            while(low < high){
                int sum = nums[i] + nums[low] + nums[high];
                int curr_diff = abs(target-sum);

                if(curr_diff < abs(diff))
                {
                    diff = target - sum;
                }

                if(sum < target)
                {
                    low++;
                }
                else
                {
                    high--;
                }
            }
        }
        return target-diff;
    }

};
```

### **Notes**

* Again a place where 2 pointer approach comes in handy.

## **[Sort Colors](sort_colors.md)**

## **[Maximum Subarray](maximum_subarray.md)**

## **[Longest Substring Without Repeating Characters](longest_substring.md)**

## **[Search Insert Position](search_insert_pos.md)**

## **[Combinations](combinations.md)**

## **[Letter Combinations of a Phone Number](letter_combinations.md)**

## **[Subsets](subsets.md)**

## **[Word Break](word_break.md)**

## **[Implement Trie](trie.md)**

## **[Linked Cycle List 2](Linked_List_cycle2.md)**

## **[LRU Cache](LRU_Cache.md)**

## **[Rotate Image](rotate_img.md)**

## **[Reverse Words in a String](reverse_words.md)**

## **[Longest Palindromic Substring](longest_palindrome.md)**

## **[Course Schedule II](course_schedule2.md)**

## **[Permutations](permutations.md)**

## **[Coin Change 2](coin_change2.md)**

## **[Container with Most Water](container.md)**

## **[Depth First Search](dfs.md)**

## **[Breadth First Search](bfs.md)**

## **[Possible Bipartition](bipartition.md)**

## **[Number of Islands](num_islands.md)**

## **[Iterative Traversal Binary Tree](post_order.md)**

## **[Diameter of Binary Tree](diameter_binaryTree.md)**

## **[Lowest Common Ancestor Binary Tree](lca_binaryTree.md)**
