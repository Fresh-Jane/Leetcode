### 671. Second Minimum Node In a Binary Tree (Easy)

https://leetcode.com/problems/second-minimum-node-in-a-binary-tree/

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
    int findSecondMinimumValue(TreeNode* root) {
        if (!root) return -1;
        int res = -1;
        preorder(root, root->val, res);
        return res;
    }
    void preorder(TreeNode* root, int minv, int& res) {
        if (!root) return;
        if (root->val > minv) res = res == -1 ? root->val : min(res, root->val);
        preorder(root->left, minv, res);
        preorder(root->right, minv, res);
    }
};
```
