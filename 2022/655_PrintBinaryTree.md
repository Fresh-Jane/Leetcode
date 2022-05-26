### 655. Print Binary Tree (Medium)

https://leetcode.com/problems/print-binary-tree/

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
    int height;
    vector<vector<string>> printTree(TreeNode* root) {
        height = max_height(root);
        int row = height+1, col = pow(2, height+1)-1;
        vector<vector<string>> res(row, vector<string>(col, ""));
        dfs(root, 0, (col-1)/2, res);
        return res;
    }
    void dfs(TreeNode* root, int r, int c, vector<vector<string>>& res) {
        if (!root) return;
        res[r][c] = to_string(root->val);
        if (root->left) dfs(root->left, r+1, c-pow(2, height-r-1), res);
        if (root->right) dfs(root->right, r+1, c+pow(2, height-r-1), res);
    }
    int max_height(TreeNode* root) {
        if (!root) return -1;
        return max(max_height(root->left), max_height(root->right)) + 1;
    }
};
```
