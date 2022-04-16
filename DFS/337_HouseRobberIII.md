### 337. House Robber III (Medium)

https://leetcode.com/problems/house-robber-iii/

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
// DFS
// Postorder, return 2 number for rob or no_rob for each node. Calculate the parent node status using the children nodes return values.
class Solution {
public:
    int rob(TreeNode* root) {
        vector<int> res = dfs(root);
        return max(res[0], res[1]);
    }
    vector<int> dfs(TreeNode* root) {
        if (!root) return {0, 0};
        auto l = dfs(root->left);
        auto r = dfs(root->right);
        vector<int> cur(2);
        cur[0] = max(l[0], l[1]) + max(r[0], r[1]);
        cur[1] = root->val + l[0] + r[0];
        return cur;
    }
};
```
