### 257. Binary Tree Paths (Easy)

https://leetcode.com/problems/binary-tree-paths/

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
    vector<string> binaryTreePaths(TreeNode* root) {
        if (!root) return {};
        vector<string> all_path;
        dfs(root, to_string(root->val), &all_path);
        return all_path;
    }
    void dfs(TreeNode* root, string path, vector<string>* all_path) {
        if (!root->left && !root->right) {
            all_path->push_back(path);
            return;
        }
        if (root->left) dfs(root->left, path+"->"+to_string(root->left->val), all_path);
        if (root->right) dfs(root->right, path+"->"+to_string(root->right->val), all_path);
    }
};
```
