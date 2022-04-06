### 1740. Find Distance in a Binary Tree (Medium)

https://leetcode.com/problems/find-distance-in-a-binary-tree/

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
    TreeNode* findLca(TreeNode* root, int p, int q) {
        if (!root) return root;
        if (root->val == p || root->val == q) return root;
        TreeNode* left = findLca(root->left, p, q);
        TreeNode* right = findLca(root->right, p, q);
        if (left && right) return root;
        return left ? left : right; 
    }
    int findDistance(TreeNode* root, int p, int q) {
        TreeNode* lca = findLca(root, p, q);
        int dp = -1, dq = -1, l = 0;
        queue<TreeNode*> que;
        que.push(lca);
        while(!que.empty() && (dp == -1 || dq == -1)) {
            int len = que.size();
            for (int i = 0; i < len; ++i) {
                auto cur = que.front(); que.pop();
                if (cur->val == p) dp = l;
                if (cur->val == q) dq = l;
                if (cur->left) que.push(cur->left);
                if (cur->right) que.push(cur->right);
            }
            l++;
        }
        return dp + dq;
    }
};
```
