### 1315. Sum of Nodes with Even-Valued Grandparent (Medium)

https://leetcode.com/problems/sum-of-nodes-with-even-valued-grandparent/

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
    int sumEvenGrandparent(TreeNode* root, int p = 1, int gp = 1) {
        return root ? sumEvenGrandparent(root->left, root->val, p)
            + sumEvenGrandparent(root->right, root->val, p)
            + (gp % 2 ? 0 : root->val) : 0;
    }
};

// BFS
class Solution {
public:
    int sumEvenGrandparent(TreeNode* root) {
        queue<TreeNode*> q;
        q.push(root);
        int res = 0;
        while(!q.empty()) {
            TreeNode* cur = q.front();
            q.pop();
            if (cur->left) {
                q.push(cur->left);
                if (cur->val % 2 == 0) {
                    res += cur->left->left ? cur->left->left->val : 0;
                    res += cur->left->right ? cur->left->right->val : 0;
                }
            }
            if (cur->right) {
                q.push(cur->right);
                if (cur->val % 2 == 0) {
                    res += cur->right->left ? cur->right->left->val : 0;
                    res += cur->right->right ? cur->right->right->val : 0;
                }
            }
        }
        return res;
    }
};
```
