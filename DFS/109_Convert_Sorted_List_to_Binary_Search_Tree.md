### 109. Convert Sorted List to Binary Search Tree (Medium)

Given a singly linked list where elements are sorted in ascending order, convert it to a height balanced BST.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.

Example:

Given the sorted linked list: [-10,-3,0,5,9],

One possible answer is: [0,-3,9,-10,null,5], which represents the following height balanced BST:

```
      0
     / \
   -3   9
   /   /
 -10  5
```
```
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
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
    TreeNode* sortedSubListToBST(ListNode*& head, int l, int r) {
        if (l > r) return nullptr;
        const int mid = (r + l) / 2;
        TreeNode* left = sortedSubListToBST(head, l, mid - 1);
        TreeNode* root = new TreeNode(head->val);
        root->left = left;
        head = head->next;
        root->right = sortedSubListToBST(head, mid + 1, r);
        return root;
    }
    TreeNode* sortedListToBST(ListNode* head) {
        int len = 0;
        ListNode* cur = head;
        while(cur) {
            len++;
            cur = cur->next;
        }
        return sortedSubListToBST(head, 0, len - 1);
    }
};
```
