### 979. Distribute Coins in Binary Tree (Medium)

https://leetcode.com/problems/distribute-coins-in-binary-tree/

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
// The excess of leaves can be regarded as leaf->val-1, and count of move is abs(excess).
// For the parent nodes, the excess can be regarded as node->val + excess(left) + excess(right) - 1. 
// The number of move should be added for each node.
class Solution {
public:
    int res;
    int distributeCoins(TreeNode* root) {
        res = 0;
        postorder(root);
        return res;
    }
    int postorder(TreeNode* root) {
        if (!root) return 0;
        int left = postorder(root->left);
        int right = postorder(root->right);
        res += abs(left) + abs(right);
        return root->val + left + right - 1;
    }
};
```
