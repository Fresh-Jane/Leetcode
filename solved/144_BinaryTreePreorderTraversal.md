### 144. Binary Tree Preorder Traversal (Easy)

https://leetcode.com/problems/binary-tree-preorder-traversal/description/

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

// Recursive
class Solution {
public:
    vector<int> res;
    vector<int> preorderTraversal(TreeNode* root) {
        preorder(root);
        return res;
    }
    void preorder(TreeNode* root) {
        if (!root) return;
        res.push_back(root->val);
        preorder(root->left);
        preorder(root->right);
    }
};

// Iterative
class Solution {
public:
    vector<int> preorderTraversal(TreeNode* root) {
        if (!root) return {};
        vector<int> res;
        stack<TreeNode*> st;
        st.push(root);
        while (!st.empty()) {
            TreeNode* cur = st.top(); st.pop();
            res.push_back(cur->val);
            if (cur->right) st.push(cur->right);
            if (cur->left) st.push(cur->left);
        }
        return res;
    }
};
```
