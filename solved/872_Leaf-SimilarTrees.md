### 872. Leaf-Similar Trees (Easy)

https://leetcode.com/problems/leaf-similar-trees/

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
    void getLeaf(TreeNode* root, vector<int>& leaf) {
        if (!root) return;
        if (!root->left && !root->right) {
            leaf.push_back(root->val);
            return;
        }
        if (root->left) getLeaf(root->left, leaf);
        if (root->right) getLeaf(root->right, leaf);
    }
    bool leafSimilar(TreeNode* root1, TreeNode* root2) {
        vector<int> l1, l2;
        getLeaf(root1, l1);
        getLeaf(root2, l2);
        return l1 == l2;
    }
};
```
