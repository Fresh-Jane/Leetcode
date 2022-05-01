### 222. Count Complete Tree Nodes (Medium)

https://leetcode.com/problems/count-complete-tree-nodes/

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

// Solution : divide and conquer, O((logn)^2)
class Solution {
public:
    int countNodes(TreeNode* root) {
        if (!root) return 0;
        int left_num = 0, right_num = 0;
        for (TreeNode* p = root; p; p = p->left) left_num++;
        for (TreeNode* p = root; p; p = p->right) right_num++;
        if (left_num == right_num) return pow(2, left_num) - 1;
        return 1 + countNodes(root->left) + countNodes(root->right);
    }
};
```
