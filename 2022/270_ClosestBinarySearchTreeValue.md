### 270. Closest Binary Search Tree Value (Easy)

https://leetcode.com/problems/closest-binary-search-tree-value/

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
    int closestValue(TreeNode* root, double target) {
        int res = root->val;
        dfs(root, target, res);
        return res;
    }
    void dfs(TreeNode* root, double target, int& res) {
        if (!root) return;
        if (abs(root->val - target) < abs(res - target)) res = root->val;
        if (root->val > target) dfs(root->left, target, res);
        if (root->val < target) dfs(root->right, target, res);
    }
};
```
