### 285. Inorder Successor in BST (Medium)

https://leetcode.com/problems/inorder-successor-in-bst/

```
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
// DFS
// Recursion
class Solution {
public:
    TreeNode* inorderSuccessor(TreeNode* root, TreeNode* p) {
        if (!root || !p) return NULL;
        if (root->val <= p->val) return inorderSuccessor(root->right, p);
        else {
            TreeNode* left = inorderSuccessor(root->left, p);
            return left ? left : root;
        }
    }
};
// Iteration
class Solution {
public:
    TreeNode* inorderSuccessor(TreeNode* root, TreeNode* p) {
        if (!root || !p) return NULL;
        TreeNode *pre = NULL, *cur = root;
        while(cur) {
            if (cur->val > p->val) {
                pre = cur;
                cur = cur->left;
            } else cur = cur->right;
        }
        return pre;
    }
};
```
