### 107. Binary Tree Level Order Traversal II (Medium)

https://leetcode.com/problems/binary-tree-level-order-traversal-ii/description/

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
    vector<vector<int>> levelOrderBottom(TreeNode* root) {
        if (!root) return {};
        vector<vector<int>> res;
        queue<TreeNode*> q;
        q.push(root);
        while(!q.empty()) {
            int len = q.size();
            res.push_back({});
            res.back().reserve(len);
            while(len--) {
                TreeNode* cur = q.front(); q.pop();
                res.back().push_back(cur->val);
                if (cur->left) q.push(cur->left);
                if (cur->right) q.push(cur->right);
            }
        }
        reverse(res.begin(), res.end());
        return res;
    }
};
```
