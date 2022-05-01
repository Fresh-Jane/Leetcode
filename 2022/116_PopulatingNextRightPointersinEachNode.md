### 116. Populating Next Right Pointers in Each Node (Medium)

https://leetcode.com/problems/populating-next-right-pointers-in-each-node/

```
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* left;
    Node* right;
    Node* next;

    Node() : val(0), left(NULL), right(NULL), next(NULL) {}

    Node(int _val) : val(_val), left(NULL), right(NULL), next(NULL) {}

    Node(int _val, Node* _left, Node* _right, Node* _next)
        : val(_val), left(_left), right(_right), next(_next) {}
};
*/
// BFS
class Solution {
public:
    Node* connect(Node* root) {
        if (!root) return root;
        queue<Node*> q;
        q.push(root);
        Node* pre = NULL;
        while (!q.empty()) {
            int len = q.size();
            while(len--) {
                Node* cur = q.front(); q.pop();
                if (pre != NULL) pre->next = cur;
                if(len) pre = cur;
                else {
                    cur->next = NULL;
                    pre = NULL;
                }
                if (cur->left != NULL) q.push(cur->left);
                if (cur->right != NULL) q.push(cur->right);
            }
        }
        return root;
    }
};

// For the tree is perfect tree, so just recursion connect it. 
class Solution {
public:
    Node* connect(Node* root) {
        if (!root) return root;
        if (root->left) {
            root->left->next = root->right;
            root->right->next = root->next ? root->next->left : NULL;
        }
        connect(root->left);
        connect(root->right);
        return root;
    }
};
```
