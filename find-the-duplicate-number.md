# Problem: [find-the-duplicate-number](https://leetcode.com/problems/find-the-duplicate-number/)

## Language Used: C++

## Solution 1


Since we can use only O(1) extra space and Running time should be less than O(n^2)

So brute force won't be the best solution

Let's sort the array in O(nlog(n))

Iterate in O(n) and if we find two adjacent same elements then we return the element


```c++
#include<math.h>
class Solution {
public:
    int findDuplicate(vector<int>& nums) {

        //Sorting array
        sort(nums.begin(), nums.end());
        
        //Finding duplicate
        for(int i = 0; i<nums.size()-1; i++){
            if(nums[i] == nums[i+1]){
                return nums[i];
            }
        }
        
        return -1;
    }
       
};

```

***Time Complexity: O(nlog(n))***

***Space complexity: O(1)***

## Solution 2

The above solution works. But we can leverage the fact that the integers are only between 1 and n.
So, iterate in the vector. And mark the index represented as value to negative.

[1,3,4,2,2]

abs(1)

[-1,3,4,2,2]

abs(3)

[-1,3,-4,2,2]

abs(-4)

[-1,3,-4,-2,2]

abs(-2)

[-1,-3,-4,-2,2]

abs(2)

Now at index 2, we already have a negative value therefore, 2 is the repetitive number.

```c++

#include<math.h>

class Solution {
public:

    int findDuplicate(vector<int>& nums) {
        
        
        for(int i = 0; i<nums.size(); i++){
            
            if(nums[abs(nums[i]) - 1] < 0){
                
                return abs(nums[i]);
            }
                    
            else{
                nums[abs(nums[i]) - 1] *= -1;
            }
        }
    ******
        return -1;
        
    }
};

```

***Time Complexity: O(n)***

***Space complexity: O(1)***