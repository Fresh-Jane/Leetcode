### 272. Closest Binary Search Tree Value II (Hard)

https://leetcode.com/problems/closest-binary-search-tree-value-ii/

```
// Intraversal
// O(N)
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
    vector<int> closestKValues(TreeNode* root, double target, int k) {
        inorder_dfs(root, target, k);
        return {q.begin(), q.end()};
    }
private:
    void inorder_dfs(TreeNode* root, double target, int k) {
        if (!root) return;
        inorder_dfs(root->left, target, k);
        if (q.size() < k) q.push_back(root->val);
        else {
            if (fabs(root->val - target) < fabs(q.front() - target)) {
                q.pop_front();
                q.push_back(root->val);
            } else return;
        }
        inorder_dfs(root->right, target, k);
    }
    deque<int> q;
};
```
