### 987. Vertical Order Traversal of a Binary Tree (Hard)

https://leetcode.com/problems/vertical-order-traversal-of-a-binary-tree/

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
// Self: BFS
class Solution {
public:
    vector<vector<int>> verticalTraversal(TreeNode* root) {
        vector<vector<int>> res;
        if (!root) return res;
        map<int, vector<int>> m;
        queue<pair<TreeNode*, int>> q;
        q.push({root, 0});
        while(!q.empty()) {
            int len = q.size();
            map<int, vector<int>> sub_m;
            while(len--) {
                TreeNode* cur_n = q.front().first;
                int cur_col = q.front().second;
                q.pop();
                sub_m[cur_col].push_back(cur_n->val);
                if (cur_n->left) q.push({cur_n->left, cur_col - 1});
                if (cur_n->right) q.push({cur_n->right, cur_col + 1});
            }
            for (auto sp : sub_m) {
                const int cur = sp.first;
                vector<int> cur_vec = sp.second;
                sort(cur_vec.begin(), cur_vec.end());
                m[cur].insert(m[cur].end(), cur_vec.begin(), cur_vec.end());
            }
        }
        for (auto p : m) res.push_back(p.second);
        return res;
    }
};
```
