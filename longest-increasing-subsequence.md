# Problem: [longest-increasing-subsequence](https://leetcode.com/problems/longest-increasing-subsequence/submissions/)

## Language Used: Python

## Solution 1: Dynamic Programming


We need to find the longest increasing subsequence

Note a that a subsequence need not be continuous.

For [10,9,2,5,3,7,101], LIS can be [2,3,7,101]

There can be multiple solutions.


[10,9,2,5,3,7,101]

Create an array LIS which will store the max counts of subsequences

For DP we need to identify the `subproblem`.
Consider the example above:

We know that every element can form a sequence of length 1. 
i.e if we take 10, then it's a subsequence in itself of length 1

So initialize an array LIS if length equal to that of nums with the value 1.

Current Element: 10
No element less than 10. LIS[0] remains as it is

LIS = [1,1,1,1,1,1,1]

Current Element: 9
Previous elements: 10, Greater than 9, LIS[1] remains as it is

LIS = [1,1,1,1,1,1,1]

Current Element: 2
Previous elements: 10, 9, Greater than 2, LIS[2] remains as it is

LIS = [1,1,1,1,1,1,1]


Current Element: 5
Previous elements: 10, 9, 2 
Now we see that 5 is greater than 2.
So what if 2, 5 forms a subsequence?
Therefore, LIS[3] = LIS[2]+1

LIS = [1,1,1,2,1,1,1]
  
Current Element: 3
Previous elements: 10, 9, 2, 5
Now we see that 3 is greater than 2.
So what if 2, 3 forms a subsequence?
Therefore, LIS[4] = LIS[2]+1

LIS = [1,1,1,2,2,1,1]

Current Element: 7
Previous elements: 10, 9, 2, 5, 3
Now we see that 3 is greater than 2.
So what if 2, 7 forms a subsequence?
Therefore, LIS[5] = LIS[2]+1
5 is also less than 7
So we can also include in the subsequence of 5
i.e 2, 5, 7
LIS[5] = LIS[3]+1
Repeat this for all the elements less than the current element

LIS = [1,1,1,2,2,3,1]

Current Element: 101
Previous elements: 10, 9, 2, 5, 3, 7
We can also include in the subsequence of 7
i.e 2, 5, 7, 101
LIS[6] = LIS[5]+1

LIS = [1,1,1,2,2,3,4]

We can finally say that maximum length is 4

```python
class Solution:
    

    # 1. Using dynamic programming: O(n^2)
    
    
    def lengthOfLIS(self, nums: List[int]) -> int:

        n = len(nums)
        
        if(n == 0):
            return 0
        
        LIS = [1]*(n)
        
        maxx = 1
        
        for i in range(n):
            for j in range(i):

                # if the current element(i) is greater than the previous elements(j)
                # and the LIS length of current element: LIS[i]
                # is less than the LIS length +1 of previous elements: LIS[j]+1
                #LIS[j] + 1 => considering previous subsequence and adding current element to it

                if(nums[j] < nums[i] and LIS[j]+1 > LIS[i]):
                    LIS[i] = LIS[j] + 1
                    if(LIS[i] > maxx):
                        maxx = LIS[i]
        return maxx
        
    # We shall look into another approach later: O(nlog(n))

```

***Time Complexity: O(n^2)***

***Space complexity: O(n)***