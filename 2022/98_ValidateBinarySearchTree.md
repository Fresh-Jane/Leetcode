### 98. Validate Binary Search Tree (Medium)

https://leetcode.com/problems/validate-binary-search-tree/

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

// inorder traverse, stack
class Solution {
public:
    bool isValidBST(TreeNode* root) {
        if (!root) return true;
        TreeNode* pre = NULL;
        TreeNode* cur = root;
        stack<TreeNode*> st;
        while(cur || !st.empty()) {
            while(cur) {
                st.push(cur);
                cur = cur->left;
            }
            cur = st.top(); st.pop();
            if (pre && cur->val <= pre->val) return false;
            pre = cur;
            cur = cur->right;
        }
        return true;
    }
};

// determine a node's value if in valid range, recursive
class Solution {
public:
    bool isValidBST(TreeNode* root) {
        return dfs(root, LONG_MIN, LONG_MAX);
    }
    bool dfs(TreeNode* root, long long low, long long high) {
        if (!root) return true;
        return root->val > low && root->val < high &&
               dfs(root->left, low, root->val) &&
               dfs(root->right, root->val, high);
    }
};
```
