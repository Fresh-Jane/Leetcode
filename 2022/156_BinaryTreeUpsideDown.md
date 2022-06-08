### 156. Binary Tree Upside Down (Medium)

https://leetcode.com/problems/binary-tree-upside-down/

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
// We can use recursive DFS to solve this problem, the main problem is how to record the old connection after we move the pointer.
// The best way is to move from the new root.
// First, we can find the left most node, it will be the root of the whole upside tree.
// Then, we can move the pointer one by one following the rules.
class Solution {
public:
    TreeNode* upsideDownBinaryTree(TreeNode* root) {
        if (!root || (!root->left && !root->right)) return root;
        TreeNode* newRoot = upsideDownBinaryTree(root->left);
        root->left->right = root;
        root->left->left = root->right;
        root->left = root->right = nullptr;
        return newRoot;
    }
};
```
