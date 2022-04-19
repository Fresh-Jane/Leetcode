### 2096. Step-By-Step Directions From a Binary Tree Node to Another (Medium)

https://leetcode.com/problems/step-by-step-directions-from-a-binary-tree-node-to-another/

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
// Get the LCA first, dfs to get the path from lca to start and end. For we only go upper from start to lca, so we can convert the start to lca easily. 
class Solution {
public:
    TreeNode* getLCA(TreeNode* cur, int s, int e) {
        if (!cur) return NULL;
        if (cur->val == s || cur->val == e) return cur;
        TreeNode* l = getLCA(cur->left, s, e);
        TreeNode* r = getLCA(cur->right, s, e);
        if (l && r) return cur;
        return l ? l : r;
    }
    
    bool getPath(TreeNode* root, string& path, int n) {
        if (!root) return false;
        if (root->val == n) return true;
        path.push_back('L');
        if (getPath(root->left, path, n)) return true;
        path.pop_back();
        path.push_back('R');
        if (getPath(root->right, path, n)) return true;
        path.pop_back();
        return false;
    }
    
    string getDirections(TreeNode* root, int startValue, int destValue) {
        TreeNode* lca = getLCA(root, startValue, destValue);
        string lca_s, lca_e;
        getPath(lca, lca_s, startValue);
        getPath(lca, lca_e, destValue);
        for (auto& c : lca_s) c = 'U';
        return lca_s + lca_e;
    }
};
```
