### 549. Binary Tree Longest Consecutive Sequence II (Medium)

https://leetcode.com/problems/binary-tree-longest-consecutive-sequence-ii/

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
    int res = 0;
    int longestConsecutive(TreeNode* root) {
        dfs(root);
        return res;
    }
    pair<int, int> dfs(TreeNode* cur) {
        if (!cur) return {0, 0};
        auto [linc, ldec] = dfs(cur->left);
        auto [rinc, rdec] = dfs(cur->right);
        if (cur->left && cur->val - cur->left->val == 1) linc += 1; else linc = 1;
        if (cur->left && cur->left->val - cur->val == 1) ldec += 1; else ldec = 1;
        if (cur->right && cur->val - cur->right->val == 1) rinc += 1; else rinc = 1;
        if (cur->right && cur->right->val - cur->val == 1) rdec += 1; else rdec = 1;
        res = max(res, max(linc+rdec-1, ldec+rinc-1));
        return {max(linc, rinc), max(ldec, rdec)};
    }
};
```
