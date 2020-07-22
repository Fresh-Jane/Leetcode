### 111. Minimum Depth of Binary Tree (Easy)

Given a binary tree, find its minimum depth.

The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.

Note: A leaf is a node with no children.

Example:

Given binary tree [3,9,20,null,null,15,7],

```
    3
   / \
  9  20
    /  \
   15   7
```
return its minimum depth = 2.
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
    int minDepth(TreeNode* root) {
        if (!root) return 0;
        const int l = minDepth(root->left);
        const int r = minDepth(root->right);
        return 1 + (min(l, r) ? min(l, r) : max(l, r));
    }
};

// BFS
class Solution 2 {
public:
    int minDepth(TreeNode* root) {
        if (root == NULL) return 0;
        queue<TreeNode*> Q;
        Q.push(root);
        int i = 0;
        while (!Q.empty()) {
            i++;
            int k = Q.size();
            for (int j=0; j<k; j++) {
                TreeNode* rt = Q.front();
                if (rt->left) Q.push(rt->left);
                if (rt->right) Q.push(rt->right);
                Q.pop();
                if (rt->left==NULL && rt->right==NULL) return i;
            }
        }
        return -1; //For the compiler thing. The code never runs here.
    }
};
```
