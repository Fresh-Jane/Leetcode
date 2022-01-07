### 1110. Delete Nodes And Return Forest (Medium)

https://leetcode.com/problems/delete-nodes-and-return-forest/

Given the root of a binary tree, each node in the tree has a distinct value.

After deleting all nodes with a value in to_delete, we are left with a forest (a disjoint union of trees).

Return the roots of the trees in the remaining forest. You may return the result in any order.

Example 1:

```
Input: root = [1,2,3,4,5,6,7], to_delete = [3,5]
Output: [[1,2,null,4],[6],[7]]
```
Example 2:

```
Input: root = [1,2,4,null,3], to_delete = [3]
Output: [[1,2,4]]
```

Constraints:

- The number of nodes in the given tree is at most 1000.
- Each node has a distinct value between 1 and 1000.
- to_delete.length <= 1000
- to_delete contains distinct values between 1 and 1000.

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
    TreeNode* dfs(unordered_set<int>& delete_set, vector<TreeNode*>& res, TreeNode* cur, bool is_root) {
        if (cur == nullptr) return nullptr;
        const bool is_deleted = delete_set.find(cur->val) != delete_set.end();
        if (is_root && !is_deleted) res.push_back(cur);
        cur->left = dfs(delete_set, res, cur->left, is_deleted);
        cur->right = dfs(delete_set, res, cur->right, is_deleted);
        return is_deleted ? nullptr : cur;
    }
    
    vector<TreeNode*> delNodes(TreeNode* root, vector<int>& to_delete) {
        unordered_set<int> delete_set(to_delete.begin(), to_delete.end());
        vector<TreeNode*> res;
        dfs(delete_set, res, root, true);
        return res;
    }
};
```
