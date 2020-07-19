### 105. Construct Binary Tree from Preorder and Inorder Traversal (Medium)

Given preorder and inorder traversal of a tree, construct the binary tree.

Note:
You may assume that duplicates do not exist in the tree.

For example, given

```
preorder = [3,9,20,15,7]
inorder = [9,3,15,20,7]
```
Return the following binary tree:

```
    3
   / \
  9  20
    /  \
   15   7
```
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
    TreeNode* buildSubTree(vector<int>& preorder, vector<int>& inorder, int pre_l, int pre_r, int in_l, int in_r) {
        if (pre_r < pre_l || in_r < in_l) return nullptr;
        int left_size = 0;
        for (int i = in_l; i <= in_r; ++i) {
            if (inorder[i] == preorder[pre_l]){
                left_size = i - in_l;
                break;
            } 
        }
        TreeNode* res = new TreeNode(preorder[pre_l]);
        res->left = buildSubTree(preorder, inorder, 
                                 pre_l + 1, pre_l + left_size,
                                 in_l, in_l + left_size - 1);
        res->right = buildSubTree(preorder, inorder, 
                                  pre_l + left_size + 1, pre_r,
                                  in_l + left_size + 1, in_r);
        return res;
    }
    
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        const int len = preorder.size();
        return buildSubTree(preorder, inorder, 0, len - 1, 0, len - 1);
    }
};
```
