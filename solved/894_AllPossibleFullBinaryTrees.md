### 894. All Possible Full Binary Trees (Medium)

https://leetcode.com/problems/all-possible-full-binary-trees/

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
// Recursive
// The count of nodes in the valid full binary trees should be odd.
class Solution {
public:
    vector<TreeNode*> allPossibleFBT(int n) {
        if (n&1 == 0) return {};
        if (n == 1) return {new TreeNode(0)};
        vector<TreeNode*> res;
        for (int i = 2; i <= n; i += 2) {
            for (TreeNode* ll : allPossibleFBT(i - 1)) {
                for (TreeNode* rr : allPossibleFBT(n - i)) {
                    TreeNode* head = new TreeNode(0);
                    head->left = ll;
                    head->right = rr;
                    res.push_back(head);
                }
            }
        }
        return res;
    }
};
```
