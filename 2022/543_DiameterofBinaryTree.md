### 543. Diameter of Binary Tree (Easy)

https://leetcode.com/problems/diameter-of-binary-tree/

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
    int diameterOfBinaryTree(TreeNode* root) {
        if (!root) return 0;
        int res = 1;
        postorder(root, res);
        return res - 1;
    }
    
    int postorder(TreeNode* root, int& res) {
        if (!root) return 0;
        int left = postorder(root->left, res);
        int right = postorder(root->right, res);
        res = max(res, 1 + left + right);
        return 1 + max(left, right);
    }
};
```
