### 129. Sum Root to Leaf Numbers (Medium)

https://leetcode.com/problems/sum-root-to-leaf-numbers/

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
// Preorder
class Solution {
public:
    int res = 0;
    int sumNumbers(TreeNode* root) {
        dfs(root, 0);
        return res;
    }
    void dfs(TreeNode* cur, int cur_r) {
        if (!cur) return;
        cur_r = 10 * cur_r + cur->val;
        if (!cur->left && !cur->right) {
            res += cur_r;
            return;
        }
        if (cur->left) dfs(cur->left, cur_r);
        if (cur->right) dfs(cur->right, cur_r);
    }
};
```
