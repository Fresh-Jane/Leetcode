### 124. Binary Tree Maximum Path Sum (Hard)

https://leetcode.com/problems/binary-tree-maximum-path-sum/

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
    int maxPathSum(TreeNode* root) {
        int res = INT_MIN;
        postorder(root, res);
        return res;
    }
    int postorder(TreeNode* root, int& res) {
        if (!root) return 0;
        // If the left(or right) tree path is negtive, we don't need it.
        int left = max(0, postorder(root->left, res));
        int right = max(0, postorder(root->right, res));
        res = max(res, left+right+root->val);
        // If we want to use the parent node, we should only use one of the subtrees.
        return root->val + max(left, right);
    }
};
```
