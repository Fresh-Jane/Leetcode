### 94. Binary Tree Inorder Traversal (Easy)

https://leetcode.com/problems/binary-tree-inorder-traversal/description/

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

// Recursion
class Solution {
public:
    vector<int> res;
    vector<int> inorderTraversal(TreeNode* root) {
        inorder(root);
        return res;
    }
    void inorder(TreeNode* root) {
        if (!root) return;
        inorder(root->left);
        res.push_back(root->val);
        inorder(root->right);
    }
};

// Iterative
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        if (!root) return {};
        stack<TreeNode*> st;
        TreeNode* pt = root;
        vector<int> res;
        while(!st.empty() || pt) {
            if (pt) {
                st.push(pt);
                pt = pt->left;
            } else {
                pt = st.top(); st.pop();
                res.push_back(pt->val);
                pt = pt->right;
            }
        }
        return res;
    }
};
```
