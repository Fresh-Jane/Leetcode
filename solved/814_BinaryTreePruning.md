### 814. Binary Tree Pruning (Medium)

https://leetcode.com/problems/binary-tree-pruning/description/

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
    bool hasOne(TreeNode* root) {
        if (!root) return false;
        if (root->val == 0 && !root->left && !root->right) return false;
        bool left = hasOne(root->left);
        if (!left) root->left = nullptr;
        bool right = hasOne(root->right);
        if (!right) root->right = nullptr;
        return root->val == 1 || left ||right;
    }
    TreeNode* pruneTree(TreeNode* root) {
        return hasOne(root) ? root : nullptr;
    }
};
```
