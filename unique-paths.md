
# Problem: [unique-paths](https://leetcode.com/problems/unique-paths/)

## Language Used: C++

## Solution

Before solving this problem, first check out [minimum-path-sum](minimum-path-sum.md) problem.

The problem is a simplified version of the problem `minimum-path-sum`.

The only difference is that here we need to find number of unique paths but there you had to find minimum cost of the path.

Let's use a simple DP solution for this problem as well.

For DP the first task is to identify the subproblem.

So if I give you a point grid[i][j] along with the unique paths from grid[0][0] to reach grid[i][j-1] and grid[i-1][j] will you be able to tell me the unique to reach grid[i][j]?


```c++
class Solution {
public:
    int uniquePaths(int m, int n) {
        
        
        if(m == 0 || n==0) return 0;

        int grid[m][n];

        //We can react 0,0 to 0,0 in exactly 1 unique way.
        grid[0][0] = 1;
        
        for(int i=0; i<m; i++){
            for(int j=0; j<n; j++){
                //For the first row, we can reach any point in exatly one way, i.e. from the left point.
                if(i == 0 && j!=0){
                    grid[i][j] = 1;
                }
                //For the first col, we can reach any point in exatly one way, i.e. from the upper point.
                else if(i!=0 && j==0){
                    grid[i][j] = 1;
                }
                //For any other point, it can be reached from either left or upper node. So the total unique ways is also sum of unique ways of left and upper node. Why?
                else if(i>0 && j>0){
                    grid[i][j] = grid[i-1][j] + grid[i][j-1];
                }
                
            }
        }
        //Return unique ways to reach (m-1,n-1) to (0,0)
        return grid[m-1][n-1];
        
    }
};

```

***Time Complexity: O(m*n)***

***Space complexity: O(1)***