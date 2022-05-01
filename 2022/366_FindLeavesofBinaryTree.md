### 366. Find Leaves of Binary Tree (Medium)

https://leetcode.com/problems/find-leaves-of-binary-tree/

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
    vector<vector<int>> findLeaves(TreeNode* root) {
        vector<vector<int>> res;
        dfs(root, res);
        return res;
    }
    int dfs(TreeNode* root, vector<vector<int>>& res) {
        if (!root) return -1;
        int left = dfs(root->left, res);
        int right = dfs(root->right, res);
        int level = max(left, right) + 1;
        if (level == (int)res.size()) res.push_back({root->val});
        else res[level].push_back(root->val);
        return level;
    }
};
```
