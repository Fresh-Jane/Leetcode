### 968. Binary Tree Cameras (Hard)

https://leetcode.com/problems/binary-tree-cameras/description/

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
    int res = 0;
    enum S {
        kNoCamera = 0,
        kCamera = 1,
        kCovered = 2,
    };
    S postorder(TreeNode* root) {
        if (!root) return kCovered;
        S l = postorder(root->left);
        S r = postorder(root->right);
        if (l == kNoCamera || r == kNoCamera) {
            ++res;
            return kCamera;
        }
        if (l == kCamera || r == kCamera) {
            return kCovered;
        }
        return kNoCamera;
    }
    int minCameraCover(TreeNode* root) {
        if (postorder(root) == kNoCamera) ++res;
        return res;
    }
};
```
