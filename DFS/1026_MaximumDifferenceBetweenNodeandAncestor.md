### 1026. Maximum Difference Between Node and Ancestor (Medium)

https://leetcode.com/problems/maximum-difference-between-node-and-ancestor/

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
    int maxAncestorDiff(TreeNode* root) {
        if (!root) return 0;
        int res = 0;
        dfs(root, root->val, root->val, res);
        return res;
    }
    void dfs(TreeNode* root, int lower, int upper, int& res) {
        if (!root) return;
        res = max(max(res, abs(lower - root->val)), abs(upper - root->val));
        int n_lower = min(lower, root->val), n_upper = max(upper, root->val);
        if (root->left) dfs(root->left, n_lower, n_upper, res);
        if (root->right) dfs(root->right, n_lower, n_upper, res);
    }
};
```
