### 545. Boundary of Binary Tree (Medium)

https://leetcode.com/problems/boundary-of-binary-tree/

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
    vector<int> boundaryOfBinaryTree(TreeNode* root) {
        vector<int> res;
        if (!root) return res;
        vector<TreeNode*> lb, rb, leaves;
        if (root->left) getLeftBoundary(root->left, lb);
        else lb.push_back(root);
        if (root->right) getRightBoundary(root->right, rb);
        else rb.push_back(root);
        getLeaves(root, leaves);
        unordered_set<TreeNode*> s;
        res.push_back(root->val);
        s.insert(root);
        for (auto ln : lb) {
            if (!s.count(ln)) {
                res.push_back(ln->val);
                s.insert(ln);
            }
        }
        for (auto leaf : leaves) { 
            if (!s.count(leaf)) {
                res.push_back(leaf->val);
                s.insert(leaf);
            }
        }
        for (int i = rb.size() - 1; i >= 0; --i) {
            if (!s.count(rb[i])) {
                res.push_back(rb[i]->val);
                s.insert(rb[i]);
            }
        }
        return res;
    }
    void getLeftBoundary(TreeNode* root, vector<TreeNode*>& lb) {
        if (!root) return;
        lb.push_back(root);
        if (root->left) getLeftBoundary(root->left, lb);
        else if (root->right) getLeftBoundary(root->right, lb);
    }
    void getRightBoundary(TreeNode* root, vector<TreeNode*>& rb) {
        if (!root) return;
        rb.push_back(root);
        if (root->right) getRightBoundary(root->right, rb);
        else if (root->left) getRightBoundary(root->left, rb);
    }
    void getLeaves(TreeNode* root, vector<TreeNode*>& leaves) {
        if (!root) return;
        if (!root->left && !root->right) {
            leaves.push_back(root);
            return;
        }
        getLeaves(root->left, leaves);
        getLeaves(root->right, leaves);
    }
};
```
