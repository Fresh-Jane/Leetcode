### 662. Maximum Width of Binary Tree (Medium)

https://leetcode.com/problems/maximum-width-of-binary-tree/

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
// We can give the id to tree nodes and calculate the distance by id diff.
class Solution {
public:
    int widthOfBinaryTree(TreeNode* root) {
        if (!root) return 0;
        queue<pair<TreeNode*, unsigned int>> q;
        q.push({root, 0});
        int res = 1;
        while(!q.empty()) {
            int len = q.size();
            int l = q.front().second, r = l;
            while(len--) {
                TreeNode* cur = q.front().first;
                unsigned int c = q.front().second;
                q.pop();
                r = c;
                if (cur->left) q.push({cur->left, 2*c+1});
                if (cur->right) q.push({cur->right, 2*c+2});
            }
            res = max(res, r - l + 1);
        }
        return res;
    }
};
```
