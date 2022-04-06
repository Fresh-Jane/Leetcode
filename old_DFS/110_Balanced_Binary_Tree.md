### 110. Balanced Binary Tree (Easy)

Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as:

a binary tree in which the left and right subtrees of every node differ in height by no more than 1.

Example 1:

Given the following tree [3,9,20,null,null,15,7]:

```
    3
   / \
  9  20
    /  \
   15   7
```
Return true.

Example 2:

Given the following tree [1,2,2,3,3,null,null,4,4]:

```
       1
      / \
     2   2
    / \
   3   3
  / \
 4   4
```
Return false.

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
class Solution {
public:
    int dfs(TreeNode* root) {
        if (!root) return 0;
        const int l = dfs(root->left);
        const int r = dfs(root->right);
        if (l < 0 || r < 0 || abs(l - r) > 1) return -1;
        else return max(l, r) + 1;
    }
    bool isBalanced(TreeNode* root) {
        return dfs(root) >= 0;
    }
};
```
