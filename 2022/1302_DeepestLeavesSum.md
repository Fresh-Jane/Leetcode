### 1302. Deepest Leaves Sum (Medium)

https://leetcode.com/problems/deepest-leaves-sum/

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
    int deepestLeavesSum(TreeNode* root) {
        queue<TreeNode*> q;
        q.push(root);
        int sum = 0, len = 0;
        while(!q.empty()) {
            len = q.size();
            sum = 0;
            while(len) {
                TreeNode* cur = q.front();
                sum += cur->val;
                q.pop();
                if (cur->left) q.push(cur->left);
                if (cur->right) q.push(cur->right);
                len--;
            }
        }
        return sum;
    }
};
```
