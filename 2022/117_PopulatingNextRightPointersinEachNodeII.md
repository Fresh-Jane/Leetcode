### 117. Populating Next Right Pointers in Each Node II (Medium)

https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii/

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
        while(!q.empty()) {
            const int sum = q.size();
            int len = q.size();
            pre = NULL;
            while(len--) {
                auto cur = q.front(); q.pop();
                if (len < sum - 1) pre->next = cur;
                if (len == 0) cur->next = NULL;
                pre = cur;
                if (cur->left) q.push(cur->left);
                if (cur->right) q.push(cur->right);
            }
        }
        return root;
    }
};
```
