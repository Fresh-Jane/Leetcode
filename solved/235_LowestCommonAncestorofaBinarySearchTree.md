### 235. Lowest Common Ancestor of a Binary Search Tree (Easy)

https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/

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
// recursive
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if (!root) return NULL;
        if (p->val > q->val) return lowestCommonAncestor(root, q, p);
        if (root->val >= p->val && root->val <= q->val) return root;
        if (root->val < p->val) return lowestCommonAncestor(root->right, p, q);
        else return lowestCommonAncestor(root->left, p, q);
    }
};

// iterative
// We want to find the split node where p and q couldn't in the same subtree.
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if (!root) return NULL;
        while(root) {
            const int pv = p->val, qv = q->val, cv = root->val;
            if (pv < cv && qv < cv) root = root->left;
            else if (pv > cv && qv > cv) root = root->right;
            else return root;
        }
        return nullptr;
    }
};
```
