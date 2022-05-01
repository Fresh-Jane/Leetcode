### 199. Binary Tree Right Side View (Medium)

https://leetcode.com/problems/binary-tree-right-side-view/

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

// DFS: preorder, root->right->left
// Space: O(1)
class Solution {
public:
    void preorder(const TreeNode* root, int depth, vector<int>& res) {
        if (!root) return;
        if (depth == res.size()) res.push_back(root->val);
        preorder(root->right, depth+1, res);
        preorder(root->left, depth+1, res);
    }
    vector<int> rightSideView(TreeNode* root) {
        vector<int> res;
        preorder(root, 0, res);
        return res;
    }
};

// BFS, search according to the level.
// Space: O(n)
class Solution {
public:
    vector<int> rightSideView(TreeNode* root) {
        if (!root) return {};
        vector<int> res;
        queue<TreeNode*> q;
        q.push(root);
        while(!q.empty()) {
            int len = q.size();
            while(len--) {
                const TreeNode* cur = q.front(); q.pop();
                if (!len) res.push_back(cur->val);
                if (cur->left) q.push(cur->left);
                if (cur->right) q.push(cur->right);
            }
        }
        return res;
    }
};
```
