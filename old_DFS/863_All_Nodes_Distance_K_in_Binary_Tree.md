### 863. All Nodes Distance K in Binary Tree (Medium)

We are given a binary tree (with root node root), a target node, and an integer value K.

Return a list of the values of all nodes that have a distance K from the target node.  The answer can be returned in any order.

Example 1:

```
Input: root = [3,5,1,6,2,0,8,null,null,7,4], target = 5, K = 2

Output: [7,4,1]

Explanation: 
The nodes that are a distance 2 from the target node (with value 5)
have values 7, 4, and 1.

Note that the inputs "root" and "target" are actually TreeNodes.
The descriptions of the inputs above are just serializations of these objects.
``` 

Note:

- The given tree is non-empty.
- Each node in the tree has unique values 0 <= node.val <= 500.
- The target node is a node in the tree.
- 0 <= K <= 1000.

```
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */

// DFS to build the backEdge map
// BFS to get the K distance results
class Solution {
public:
    void dfs(TreeNode* root, TreeNode* target, unordered_map<TreeNode*, TreeNode*>& backEdge) {
        if(!root || root == target) return;
        if (root->left) {
            backEdge[root->left] = root;
            dfs(root->left, target, backEdge);
        }
        if (root->right) {
            backEdge[root->right] = root;
            dfs(root->right, target, backEdge);
        }
    }
    vector<int> distanceK(TreeNode* root, TreeNode* target, int K) {
        unordered_map<TreeNode*, TreeNode*> backEdge;
        unordered_set<TreeNode*> visited;
        dfs(root, target, backEdge);
        queue<TreeNode*> q;
        q.push(target);
        vector<int> res;
        while(!q.empty() && K >= 0) {
            int s = q.size();
            while(s--) {
                TreeNode* cur = q.front();
                q.pop();
                visited.insert(cur);
                if (K == 0) res.push_back(cur->val);
                if (backEdge.count(cur) && !visited.count(backEdge[cur])) q.push(backEdge[cur]);
                if (cur->left && !visited.count(cur->left)) q.push(cur->left);
                if (cur->right && !visited.count(cur->right)) q.push(cur->right);
            }
            K--;
        }
        return res;
    }
};
```
