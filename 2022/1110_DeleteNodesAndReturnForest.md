### 1110. Delete Nodes And Return Forest (Medium)

https://leetcode.com/problems/delete-nodes-and-return-forest/

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
    unordered_set<int> m;
    vector<TreeNode*> res;
    vector<TreeNode*> delNodes(TreeNode* root, vector<int>& to_delete) {
        m.insert(to_delete.begin(), to_delete.end());
        if (dfs(root)) res.push_back(root);
        return res;
    }
    bool dfs(TreeNode* root) {
        if (!root) return false;
        bool has_left = dfs(root->left);
        bool has_right = dfs(root->right);
        if (m.count(root->val)) {
            if (has_left) res.push_back(root->left);
            if (has_right) res.push_back(root->right);
            return false;
        } else {
            if (!has_left) root->left = NULL;
            if (!has_right) root->right = NULL;
        }
        return true;
    }
    
};
```
