### 1485. Clone Binary Tree With Random Pointer (Medium)

https://leetcode.com/problems/clone-binary-tree-with-random-pointer/

```
/**
 * Definition for a Node.
 * struct Node {
 *     int val;
 *     Node *left;
 *     Node *right;
 *     Node *random;
 *     Node() : val(0), left(nullptr), right(nullptr), random(nullptr) {}
 *     Node(int x) : val(x), left(nullptr), right(nullptr), random(nullptr) {}
 *     Node(int x, Node *left, Node *right, Node *random) : val(x), left(left), right(right), random(random) {}
 * };
 */

class Solution {
public:
    unordered_map<Node*, NodeCopy*> copied;
    NodeCopy* copyRandomBinaryTree(Node* root) {
        if (!root) return NULL;
        if (copied.count(root)) return copied[root];
        NodeCopy* newRoot = new NodeCopy(root->val);
        copied[root] = newRoot;
        newRoot->left = copyRandomBinaryTree(root->left);
        newRoot->right = copyRandomBinaryTree(root->right);
        newRoot->random = copyRandomBinaryTree(root->random);
        return newRoot;
    }
};
```
