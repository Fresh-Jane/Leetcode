### 103. Binary Tree Zigzag Level Order Traversal (Medium)

https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/

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
// BFS
// We should search the node by level and save each level values into one vector. If the level is even, reverse it. 
class Solution {
public:
    vector<vector<int>> zigzagLevelOrder(TreeNode* root) {
        vector<vector<int>> res;
        if (!root) return res;
        queue<TreeNode*> q;
        q.push(root);
        int level = 1;
        while(!q.empty()) {
            int len = q.size();
            vector<int> r;
            while(len--) {
                const TreeNode* cur = q.front(); q.pop();
                r.push_back(cur->val);
                if (cur->left) q.push(cur->left);
                if (cur->right) q.push(cur->right);
            }
            if (level % 2 == 0) reverse(r.begin(), r.end());
            res.push_back(move(r));
            level++;
        }
        return res;
    }
};
```
