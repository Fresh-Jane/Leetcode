### 101. Symmetric Tree (Easy)
Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

For example, this binary tree [1,2,2,3,4,4,3] is symmetric:

```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```

But the following [1,2,2,null,3,null,3] is not:

```
    1
   / \
  2   2
   \   \
   3    3
```
Follow up: Solve it both recursively and iteratively.

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
// Recursively
class Solution 1 {
public:
    bool isTwoSymmetric(TreeNode* l, TreeNode* r) {
        if (!l && !r) return true;
        if (!l || !r) return false;
        if (l->val != r->val) return false;
        return isTwoSymmetric(l->right, r->left) && isTwoSymmetric(l->left, r->right);
    }
    bool isSymmetric(TreeNode* root) {
        if (!root) return true;
        return isTwoSymmetric(root->left, root->right);
    }
};

// Iteratively
class Solution 2 {
public:
    bool isSymmetric(TreeNode* root) {
        if (!root) return true;
        queue<TreeNode*> ql, qr;
        ql.push(root->left);
        qr.push(root->right);
        while(!ql.empty() && !qr.empty()) {
            TreeNode* l = ql.front();
            TreeNode* r = qr.front();
            ql.pop();
            qr.pop();
            if (!l && !r) continue;
            if (!l || !r) return false;
            if (l->val != r->val) return false;
            ql.push(l->left);
            ql.push(l->right);
            qr.push(r->right);
            qr.push(r->left);
        }
        return true;
    }
};
```
