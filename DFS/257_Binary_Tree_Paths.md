257. Binary Tree Paths (Easy)

Given a binary tree, return all root-to-leaf paths.

Note: A leaf is a node with no children.

Example:

```
Input:

   1
 /   \
2     3
 \
  5

Output: ["1->2->5", "1->3"]

Explanation: All root-to-leaf paths are: 1->2->5, 1->3
```
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
    void binaryTreePaths(TreeNode* root, string one_path, vector<string>& all_path) {
        if (!root->left && !root->right) {
            all_path.push_back(one_path);
            return;
        }
        if (root->left) 
            binaryTreePaths(root->left, one_path + "->" + to_string(root->left->val), all_path);
        if (root->right)
            binaryTreePaths(root->right, one_path + "->" + to_string(root->right->val), all_path);
    }
    
    vector<string> binaryTreePaths(TreeNode* root) {
        if (!root) return {};
        vector<string> all_path;
        binaryTreePaths(root, to_string(root->val), all_path);
        return all_path;
    }
};
```
