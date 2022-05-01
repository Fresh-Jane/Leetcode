### 1022. Sum of Root To Leaf Binary Numbers (Easy)

https://leetcode.com/problems/sum-of-root-to-leaf-binary-numbers/

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
    int sumRootToLeaf(TreeNode* root) {
        int res = 0;
        dfs(root, 0, res);
        return res;
    }
    void dfs(TreeNode* root, int path, int& res) {
        if (!root) return;
        path = path * 2 + root->val;
        if (!root->left && !root->right) {
            res += path;
            return;
        }
        if (root->left) dfs(root->left, path, res);
        if (root->right) dfs(root->right, path, res);
    }
};
```
