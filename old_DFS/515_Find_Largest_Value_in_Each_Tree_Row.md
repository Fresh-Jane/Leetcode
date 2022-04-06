### 515. Find Largest Value in Each Tree Row (Medium)

Given the root of a binary tree, return an array of the largest value in each row of the tree (0-indexed).

Example 1:

```
Input: root = [1,3,2,5,3,null,9]
Output: [1,3,9]
```
Example 2:

```
Input: root = [1,2,3]
Output: [1,3]
```
Example 3:

```
Input: root = [1]
Output: [1]
```
Example 4:

```
Input: root = [1,null,2]
Output: [1,2]
```
Example 5:

```
Input: root = []
Output: []
```

Constraints:

- The number of nodes in the tree will be in the range [0, 104].
- -2^31 <= Node.val <= 2^31 - 1

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
class Solution 1 {
public:
    vector<int> largestValues(TreeNode* root) {
        if (!root) return {};
        vector<int> res;
        queue<TreeNode*> q;
        q.push(root);
        int max_val;
        while(!q.empty()) {
            int cnt = q.size();
            max_val = q.front()->val;
            while(cnt--) {
                TreeNode* p = q.front(); q.pop();
                if(p->val > max_val) max_val = p->val;
                if(p->left) q.push(p->left);
                if(p->right) q.push(p->right);
            }
            res.push_back(max_val);
        }
        return res;
    }
};

// DFS
class Solution 2 {
public:
    void dfs(TreeNode* root, int level, vector<int>& res) {
        if (level == res.size()) res.push_back(root->val);
        if (root->val > res[level]) res[level] = root->val;
        if (root->left) dfs(root->left, level+1, res);
        if (root->right) dfs(root->right, level+1, res);
    }
    
    vector<int> largestValues(TreeNode* root) {
        if (!root) return {};
        vector<int> res;
        dfs(root, 0, res);
        return res;
    }
};
```
