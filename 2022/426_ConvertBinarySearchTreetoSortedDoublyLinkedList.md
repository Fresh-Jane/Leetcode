### 426. Convert Binary Search Tree to Sorted Doubly Linked List (Medium)

https://leetcode.com/problems/convert-binary-search-tree-to-sorted-doubly-linked-list/

```
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* left;
    Node* right;

    Node() {}

    Node(int _val) {
        val = _val;
        left = NULL;
        right = NULL;
    }

    Node(int _val, Node* _left, Node* _right) {
        val = _val;
        left = _left;
        right = _right;
    }
};
*/

class Solution {
public:
    Node* pre;
    Node* first;
    Node* treeToDoublyList(Node* root) {
        if (!root) return root;
        pre = nullptr;
        first = nullptr;
        inorder(root);
        pre->right = first;
        first->left = pre;
        return first;
    }
    void inorder(Node* root) {
        if (!root) return;
        inorder(root->left);
        if (!first) first = root;
        if (pre) {
            pre->right = root;
            root->left = pre;
        }
        pre = root;
        inorder(root->right);
    }
    
};
```
