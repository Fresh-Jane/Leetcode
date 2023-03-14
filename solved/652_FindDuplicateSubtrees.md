### 652. Find Duplicate Subtrees (Medium)

https://leetcode.com/problems/find-duplicate-subtrees/

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
// Serialize each subtree to string and hash it.
class Solution {
public:
    unordered_map<string, int> m;
    vector<TreeNode*> res;
    vector<TreeNode*> findDuplicateSubtrees(TreeNode* root) {
        serialize(root);
        return res;
    }
    string serialize(TreeNode* root) {
        if (!root) return "#";
        string r = "(" + serialize(root->left) + to_string(root->val) + serialize(root->right) + ")";
        m[r]++;
        if (m.count(r) && m[r] == 2) res.push_back(root);
        return r;
    }
};
```
