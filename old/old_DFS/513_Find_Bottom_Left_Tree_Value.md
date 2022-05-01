### 513. Find Bottom Left Tree Value (Medium)

Given a binary tree, find the leftmost value in the last row of the tree.

Example 1:
```
Input:

    2
   / \
  1   3

Output:
1
```

Example 2:
```
Input:

        1
       / \
      2   3
     /   / \
    4   5   6
       /
      7

Output:
7
```

Note: You may assume the tree (i.e., the given root node) is not NULL.

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
class Solution 1 {
public:
    void dfs(TreeNode* root, int level, int& res, int& max_level) {
        if (max_level < level) {
            res = root->val;
            max_level = level;
        }
        if (root->left) dfs(root->left, level+1, res, max_level);
        if (root->right) dfs(root->right, level+1, res, max_level);
    }
    
    int findBottomLeftValue(TreeNode* root) {
        int res, max_level = 0;
        dfs(root, 1, res, max_level);
        return res;
    }
};

// BFS
class Solution 2 {
public:
    int findBottomLeftValue(TreeNode* root) {
        queue<TreeNode*> q;
        q.push(root);
        TreeNode* res = root;
        while(!q.empty()) {
            int num = q.size();
            res = q.front();
            while (num) {
                TreeNode* node = q.front(); q.pop();
                if (node->left) q.push(node->left);
                if (node->right) q.push(node->right);
                --num;
            }
        }
        return res->val;
    }
};
```
