# Problem: [unique-binary-search-trees](https://leetcode.com/problems/unique-binary-search-trees/)

## Language Used: C++

## Solution

There is a simple formula

Also known as `Catalan Number`

```text
T(n) = (2nCn)
      --------
       (n+1)
         
or  T(n) =     2n!
            ------------
             n!*n!*(n+1)

```


```c++
#include <math.h>

class Solution {
public:
    double fact(int n){  
        double ans = 1;	
            for(double i= 2; i<= n; i++)	
                ans *=i;
        return ans;	  
}

    int numTrees(int n) {
        
        return ceil(fact(2*n)/(pow(fact(n), 2)*(n+1)));
        
    }
};

// You can further optimise this formula:
// https://brainly.in/question/3374481

```

***Time Complexity: O(n)***

***Space complexity: O(1)***
