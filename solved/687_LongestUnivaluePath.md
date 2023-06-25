### 687. Longest Univalue Path (Medium)

https://leetcode.com/problems/longest-univalue-path/description/

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
    int longest(TreeNode* root, int& res) {
        if (!root) return 0;
        int left = longest(root->left, res);
        int right = longest(root->right, res);
        int l = (root->left && root->left->val == root->val) ? left + 1 : 0;
        int r = (root->right && root->right->val == root->val) ? right + 1 : 0;
        res = max(res, l + r);
        return max(l, r);
    }
    int longestUnivaluePath(TreeNode* root) {
        if (!root) return 0;
        int res = 0;
        longest(root, res);
        return res;
    }
};
```
