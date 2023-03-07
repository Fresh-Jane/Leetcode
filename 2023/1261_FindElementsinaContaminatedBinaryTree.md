### 1261. Find Elements in a Contaminated Binary Tree (Medium)

https://leetcode.com/problems/find-elements-in-a-contaminated-binary-tree/

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
class FindElements {
public:
    FindElements(TreeNode* root) {
        dfs(root, 0);
    }
    bool find(int target) {
        return visit_.count(target);
    }
private:
    void dfs(TreeNode* root, int x) {
        if (!root) return;
        root->val = x;
        visit_.insert(root->val);
        dfs(root->left, 2 * x + 1);
        dfs(root->right, 2 * x + 2);
    }
    unordered_set<int> visit_;
};

/**
 * Your FindElements object will be instantiated and called as such:
 * FindElements* obj = new FindElements(root);
 * bool param_1 = obj->find(target);
 */
```
