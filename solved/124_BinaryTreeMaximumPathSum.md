### 124. Binary Tree Maximum Path Sum (Hard)

https://leetcode.com/problems/binary-tree-maximum-path-sum/description/

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
    int postorder(TreeNode* root, int& res) {
        if (!root) return 0;
        int left = max(0, postorder(root->left, res));
        int right = max(0, postorder(root->right, res));
        res = max(res, left+right+root->val);
        return root->val + max(left, right);
    }
    int maxPathSum(TreeNode* root) {
        int res = INT_MIN;
        postorder(root, res);
        return res;
    }
};
```
