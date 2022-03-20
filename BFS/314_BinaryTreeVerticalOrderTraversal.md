### 314. Binary Tree Vertical Order Traversal (Medium)

https://leetcode.com/problems/binary-tree-vertical-order-traversal/

```
// BFS
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
    vector<vector<int>> verticalOrder(TreeNode* root) {
        if (!root) return {};
        map<int, vector<int>> m;
        queue<pair<TreeNode*, int>> q;
        q.push({root, 0});
        while(!q.empty()) {  // No need calculate the length of each level.
            const TreeNode* node = q.front().first;
            const int col = q.front().second;
            q.pop();
            m[col].push_back(node->val);  // map can push_back value for the inexisting key.
            if (node->left) q.push({node->left, col - 1});
            if (node->right) q.push({node->right, col + 1});
        }
        vector<vector<int>> res;
        for (const auto& p : m) res.push_back(p.second);
        return res;
    }
};
```
