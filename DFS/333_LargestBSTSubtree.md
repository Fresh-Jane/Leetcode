### 333. Largest BST Subtree (Medium)

https://leetcode.com/problems/largest-bst-subtree/

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
class Solution {
public:
    int largestBSTSubtree(TreeNode* root) {
        int res = 0;
        postorder(root, res);
        return res;
    }
    tuple<bool,int,int,int> postorder(TreeNode* cur, int& res) {
        if (!cur) return {true, 0, 0, 0};
        auto [is_l, l_lower, l_upper, l_cnt] = postorder(cur->left, res);
        auto [is_r, r_lower, r_upper, r_cnt] = postorder(cur->right, res);
        if (is_l && is_r &&
            (!cur->left || l_upper < cur->val) &&
            (!cur->right || r_lower > cur->val)) {
            res = max(res, l_cnt + 1 + r_cnt);
            return {true, 
                    cur->left ? l_lower : cur->val, 
                    cur->right ? r_upper : cur->val, 
                    l_cnt + 1 + r_cnt};
        } else {
            return {false, 0, 0, 0};
        }
    }
};
```
