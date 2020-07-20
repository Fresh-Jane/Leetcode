106. Construct Binary Tree from Inorder and Postorder Traversal (Medium)

Given inorder and postorder traversal of a tree, construct the binary tree.

Note:
You may assume that duplicates do not exist in the tree.

For example, given

inorder = [9,3,15,20,7]
postorder = [9,15,7,20,3]
Return the following binary tree:

    3
   / \
  9  20
    /  \
   15   7

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
    TreeNode* buildSubTree(vector<int>& inorder, vector<int>& postorder, int in_l, int in_r, int post_l, int post_r) {
        if (in_r < in_l || post_r < post_l) return nullptr;
        TreeNode* root = new TreeNode(postorder[post_r]);
        int left_size = 0;
        for (int i = in_l; i <= in_r; ++i) {
            if (inorder[i] == postorder[post_r]) {
                left_size = i - in_l;
                break;
            }
        }
        root->left = buildSubTree(inorder, postorder, in_l, in_l + left_size - 1, post_l, post_l + left_size - 1);
        root->right = buildSubTree(inorder, postorder, in_l + left_size + 1, in_r, post_l + left_size, post_r - 1);
        return root;
    }
    TreeNode* buildTree(vector<int>& inorder, vector<int>& postorder) {
        const int len = inorder.size();
        return buildSubTree(inorder, postorder, 0, len - 1, 0, len - 1);
    }
};
```
