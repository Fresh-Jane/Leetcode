### 199. Binary Tree Right Side View (Medium)

Given a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.

Example:

Input: [1,2,3,null,5,null,4]
Output: [1, 3, 4]
Explanation:

```
   1            <---
 /   \
2     3         <---
 \     \
  5     4       <---
```
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
// Preorder search as root-right-left, Space: O(1)
class Solution 1 {
public:
    vector<int> rightSideView(TreeNode* root) {
        vector<int> res;
        preorder(root, 0, res);
        return res;
    }
    
    void preorder(TreeNode* root, int depth, vector<int>& res) {
        if (!root) return;
        if (depth == static_cast<int>(res.size())) res.push_back(root->val);
        preorder(root->right, depth+1, res);
        preorder(root->left, depth+1, res);
    }
};

// BFS Time: O(n), Space:O(n)
class Solution 2 {
public:
    vector<int> rightSideView(TreeNode* root) {
        vector<int> res;
        if (!root) return res;
        queue<TreeNode*> q;
        q.push(root);
        int len = 0;
        while(!q.empty()) {
            len = q.size();
            while (len) {
                TreeNode* cur = q.front();
                q.pop();
                len--;
                if (cur->left) q.push(cur->left);
                if (cur->right) q.push(cur->right);
                if (!len) res.push_back(cur->val);
            }
        }
        return res;
    }
};
```
