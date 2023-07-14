### 938. Range Sum of BST (Easy)

https://leetcode.com/problems/range-sum-of-bst/description/

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
class Solution {
public:
    int rangeSumBST(TreeNode* root, int low, int high) {
        int res = 0;
        dfs(root, low, high, res);
        return res;
    }
    void dfs(TreeNode* root, int low, int high, int& res) {
        if (!root) return;
        if (root->val < low) dfs(root->right, low, high, res);
        else if (root->val > high) dfs(root->left, low, high, res);
        else {
            res += root->val;
            dfs(root->left, low, root->val, res);
            dfs(root->right, root->val, high, res);
        }
    }
};
```
