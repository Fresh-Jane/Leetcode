### 113. Path Sum II (Medium)

Given a binary tree and a sum, find all root-to-leaf paths where each path's sum equals the given sum.

Note: A leaf is a node with no children.

Example:

Given the below binary tree and sum = 22,

```
      5
     / \
    4   8
   /   / \
  11  13  4
 /  \    / \
7    2  5   1
```
Return:
```
[
   [5,4,11,2],
   [5,8,4,5]
]
```
```
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode *parent;
 *     TreeNode() : val(0), left(nullptr), right(nullptr), parent(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr), parent(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
 private: 
    void findPaths(TreeNode* root, int sum, vector<int>& path, vector<vector<int>>& paths) {
        if (!root) return;
        const int root_val = root->val;
        path.push_back(root_val);
        if (!root->left && !root->right && root_val == sum) {
            paths.push_back(path);
        } else {
            findPaths(root->left, sum - root_val, path, paths);
            findPaths(root->right, sum - root_val, path, paths);
        }
        path.pop_back();
    }
 public:
    vector<vector<int>> pathSum(TreeNode* root, int sum) {
        vector<vector<int>> paths;
        vector<int> path;
        if (!root) return paths;
        findPaths(root, sum, path, paths);
        return paths;
    }
};
```
