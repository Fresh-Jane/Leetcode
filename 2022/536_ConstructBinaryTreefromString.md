### 536. Construct Binary Tree from String (Medium)

https://leetcode.com/problems/construct-binary-tree-from-string/

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
    TreeNode* str2tree(string s) {
        int i = 0;
        return dfs(s, i);
    }
    TreeNode* dfs(const string& s, int& i) {
        const int n = s.size();
        if (i >= n) return NULL;
        int val = 0, sign = 1;
        if (s[i] == '-') {
            sign = -1;
            i++;
        }
        while(i < n && isdigit(s[i])) val = val * 10 + s[i++] - '0';
        TreeNode* root = new TreeNode(sign*val);
        if (i < n && s[i] == '(') {
            ++i;
            root->left = dfs(s, i);
            ++i;
        }
        if (i < n && s[i] == '(') {
            ++i;
            root->right = dfs(s, i);
            ++i;
        }
        return root;
    }
};
```
