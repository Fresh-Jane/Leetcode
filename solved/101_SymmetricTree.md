### 101. Symmetric Tree (Easy)

https://leetcode.com/problems/symmetric-tree/

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
// BFS
class Solution {
public:
    bool isSymmetric(TreeNode* root) {
        if (!root) return true;
        queue<TreeNode*> q;
        q.push(root);
        while(!q.empty()) {
            int len = q.size();
            vector<int> level;
            while(len--) {
                const TreeNode* cur = q.front(); q.pop();
                if (cur) {
                    level.push_back(cur->val);
                    q.push(cur->left);
                    q.push(cur->right);
                } else {
                    level.push_back(1000);
                }
            }
            int i = 0, j = level.size() - 1;
            while (i < j) {
                if (level[i] != level[j]) return false;
                i++; j--;
            }
        }
        return true;
    }
};

// Recursion
class Solution {
public:
    bool isSymmetric(TreeNode* root) {
        return !root || symmetric(root->left, root->right);
    }
    bool symmetric(TreeNode* p, TreeNode* q) {
        return (!p && !q) || (p && q && p->val == q->val && symmetric(p->left, q->right) && symmetric(p->right, q->left));
    }
    
};
```
