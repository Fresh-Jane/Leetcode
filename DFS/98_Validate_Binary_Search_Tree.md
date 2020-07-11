### 98. Validate Binary Search Tree (Medium)

Given a binary tree, determine if it is a valid binary search tree (BST).

Assume a BST is defined as follows:

- The left subtree of a node contains only nodes with keys less than the node's key.
- The right subtree of a node contains only nodes with keys greater than the node's key.
- Both the left and right subtrees must also be binary search trees.
 
Example 1:

```
    2
   / \
  1   3

Input: [2,1,3]
Output: true
```
Example 2:

```
    5
   / \
  1   4
     / \
    3   6

Input: [5,1,4,null,null,3,6]
Output: false
Explanation: The root node's value is 5 but its right child's value is 4.
```
```
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
// Time: O(n), Space: O(1)
class Solution {
public:
    bool isValidSubBST(TreeNode* root, TreeNode* min_val_node, TreeNode* max_val_node) {
        if (!root) return true;
        if ((min_val_node && root->val <= min_val_node->val) ||
            (max_val_node && root->val >= max_val_node->val)) {
            return false;
        }
        return isValidSubBST(root->left, min_val_node, root) && isValidSubBST(root->right, root, max_val_node);
    }
    
    bool isValidBST(TreeNode* root) {
        return isValidSubBST(root, nullptr, nullptr);
    }
};
```
