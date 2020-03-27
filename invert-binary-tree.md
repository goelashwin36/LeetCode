
# Problem: [invert-binary-tree](https://leetcode.com/problems/invert-binary-tree/)

## Language Used: C++

## Solution

Traverse in the tree using preorder or postorder traversal.

Swap the left and right sub trees of the node

Iterating by inorder method will be problem. Why?


```c++
class Solution {
public:
    //The function takes a node and swaps it's left and right subtrees
    void swapNodes(TreeNode* root){
        TreeNode* temp = root->left;
        root->left = root->right;
        root->right = temp;
        return;
    }
    
    TreeNode* invertTree(TreeNode* root) {
        
        //Return NULL if node is NULL
        if(root == NULL){
            return NULL;
        }
        
        // Iterating using preorder
        
        swapNodes(root);
        
        invertTree(root->left);
        
        invertTree(root->right);
        
        return root;
        
    }
};
```

***Time Complexity: O(n)***

***Space complexity: O(1) or O(n) because of recursion call stack***