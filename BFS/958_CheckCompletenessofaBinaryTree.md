### 958. Check Completeness of a Binary Tree (Medium)

https://leetcode.com/problems/check-completeness-of-a-binary-tree/

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
    bool isCompleteTree(TreeNode* root) {
        const int n = count(root);
        return check(root, 1, n);
    }
    
    int count(TreeNode* root) {
        if (!root) return 0;
        return 1 + count(root->left) + count(root->right);
    }
    
    bool check(TreeNode* root, int id, int n) {
        if (!root) return true;
        if (id > n) return false;
        return check(root->left, 2 * id, n) && check(root->right, 2 * id + 1, n);
    }
};
```
