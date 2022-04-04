### 617. Merge Two Binary Trees (Easy)

https://leetcode.com/problems/merge-two-binary-trees/

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
    TreeNode* mergeTrees(TreeNode* r1, TreeNode* r2) {
        if (!r1 && !r2) return NULL;
        if (!r1 || !r2) return r1 ? r1 : r2;
        TreeNode* r3 = new TreeNode(r1->val + r2->val);
        r3->left = mergeTrees(r1->left, r2->left);
        r3->right = mergeTrees(r1->right, r2->right);
        return r3;
    }
};
```
