### 1339. Maximum Product of Splitted Binary Tree (Medium)

https://leetcode.com/problems/maximum-product-of-splitted-binary-tree/

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

// Two pass dfs
// One pass for sum, one pass for result. The same function.
class Solution {
public:
    int MOD = 1e9 + 7;
    long long sum = 0, res = 0;
    int maxProduct(TreeNode* root) {
        sum = dfs(root);
        dfs(root);
        return res % MOD;
    }
    int dfs(TreeNode* root) {
        if (!root) return 0;
        long long sub_tree_sum = dfs(root->left) + dfs(root->right) + root->val;
        if (sum)
            res = max(res, (sum - sub_tree_sum) * sub_tree_sum);
        return sub_tree_sum;
    }
};
```
