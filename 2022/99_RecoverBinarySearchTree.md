### 99. Recover Binary Search Tree (Medium)

https://leetcode.com/problems/recover-binary-search-tree/

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
// We can get one ordered list if we use inorder traversal for a BST.
// For the mistake swap, there are two wrong order cases in the ordered list.
// And the large one in the first wrong order and the smaller one in the second wrong order should be the swap nodes we want to find.
class Solution {
public:
    void recoverTree(TreeNode* root) {
        if (!root) return;
        TreeNode *pre = NULL, *cur = root;
        TreeNode *e1 = NULL, *e2 = NULL;
        stack<TreeNode*> st;
        while(!st.empty() || cur) {
            if (cur) {
                st.push(cur);
                cur = cur->left;
            } else {
                cur = st.top(); st.pop();
                if (pre && cur->val < pre->val) {
                    if (!e1) e1 = pre;
                    e2 = cur;
                }
                pre = cur;
                cur = cur->right;
            }
        }
        swap(e1->val, e2->val);
    }
};
```
