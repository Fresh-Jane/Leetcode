### 114. Flatten Binary Tree to Linked List (Medium)

https://leetcode.com/problems/flatten-binary-tree-to-linked-list/

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

// DFS
// Iteration, preorder.
class Solution {
public:
    void flatten(TreeNode* root) {
        if (!root) return;
        stack<TreeNode*> st;
        st.push(root);
        while(!st.empty()) {
            auto t = st.top(); st.pop();
            if (t->right) st.push(t->right);
            if (t->left) st.push(t->left);
            t->left = NULL;
            if (!st.empty()) t->right = st.top();
            else t->right = NULL;
        }
    }
};

// Recursion, postorder.
class Solution {
public:
    void flatten(TreeNode* root) {
        TreeNode* next = NULL;
        dfs(root, next);
    }
    void dfs(TreeNode* cur, TreeNode*& next) {
        if (!cur) return;
        dfs(cur->right, next);
        dfs(cur->left, next);
        cur->right = next;
        cur->left = NULL;
        next = cur;
    }
};
```
