
# Problem: [minimum-path-sum](https://leetcode.com/problems/minimum-path-sum/)

## Language Used: C++

## Solution

We are given a m*n grid of non-negative integers.
We need to find minimum cost from 0,0 to reach m-1,n-1 provided we can move either right or down.

Let's use a simple DP solution for this problem.

For DP the first task is to identify the subproblem.

So if I give you a point grid[i][j] along with the minimum cost from grid[0][0] to reach grid[i][j-1] and grid[i-1][j] will you be able to tell me the minimum cost to reach grid[i][j]?

Let's take an example:

```text
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]
```

This is the original grid.
Consider point 1,1 (5).

Can you tell me minimim cost to reach 1,1 from 0,0?
We know we can move to 1,1 either from 0,1 or 1,0. 

So we need minimum cost of 0,1 and 1,0

For 0,1 it should be 1+3. Why?
For 1,0 it should be 1+1. Why?

So minimum path to 1,1 can be minimum cost from 1,0 to reach 1,1 i.e. equal to (1+1)+5 = 7

I hope you got some idea.

So now we'll iterate from 0,0 and move horizontally in rows.

For the first row, for every point we know that we can reach there only from the left node.

For the first column, for every point we can reach there only from the upper node.

All other nodes can be reached by either left or upper node.


```c++
class Solution {
public:
    int minPathSum(vector<vector<int>>& grid) {
        
        int m = grid.size();
        
        if(m == 0) return 0;
        
        int n = grid[0].size();
        
        //Iterating in rows
        for(int i=0; i<m; i++){
            //Iterating in cols
            for(int j=0; j<n; j++){

                //For the first row
                if(i == 0 && j!=0){
                    //Simply add the value of previous left node
                    //That is min cost path of previous node plus current node
                    grid[i][j] += grid[i][j-1];
                }
                //For the first column
                else if(i!=0 && j==0){
                    //Simply add the value of previous upper node
                    //That is min cost path of upper node plus current node
                    grid[i][j] += grid[i-1][j];
                }
                else if(i>0 && j>0){
                    //Find the min of cost of upper and left node
                    //Add it to current
                    int minn = (grid[i-1][j] < grid[i][j-1]) ? grid[i-1][j] : grid[i][j-1];
                    grid[i][j] += minn;
                }
                
            }
        }
        //Return the min cost to reach last node
        return grid[m-1][n-1];
        
        
    }
};

```

***Time Complexity: O(m*n)***

***Space complexity: O(1)***