### 145. Binary Tree Postorder Traversal (Easy)

https://leetcode.com/problems/binary-tree-postorder-traversal/description/

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
    vector<int> postorderTraversal(TreeNode* root) {
        postorder(root);
        return res;
    }
    void postorder(TreeNode* root) {
        if (!root) return;
        postorder(root->left);
        postorder(root->right);
        res.push_back(root->val);
    }
};

// Iterative
class Solution {
public:
    vector<int> postorderTraversal(TreeNode* root) {
        if (!root) return {};
        vector<int> res;
        stack<TreeNode*> st;
        TreeNode* pre = nullptr, *cur = root;
        while(!st.empty() || cur) {
            if (cur) {
                st.push(cur);
                cur = cur->left;
            } else {
                TreeNode* p = st.top();
                if (p->right && p->right != pre) {
                    cur = p->right;
                } else {
                    res.push_back(p->val);
                    pre = p;
                    st.pop();
                }
            }
        }
        return res;
    }
};
```
