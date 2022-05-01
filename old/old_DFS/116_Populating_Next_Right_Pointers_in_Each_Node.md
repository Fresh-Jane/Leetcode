### 116. Populating Next Right Pointers in Each Node (Medium)

You are given a perfect binary tree where all leaves are on the same level, and every parent has two children. The binary tree has the following definition:

```
struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}
```
Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to ```NULL```.

Initially, all next pointers are set to ```NULL```.

 
Follow up:

- You may only use constant extra space.
- Recursive approach is fine, you may assume implicit stack space does not count as extra space for this problem.
 

Example 1:

```
Input: root = [1,2,3,4,5,6,7]
Output: [1,#,2,3,#,4,5,6,7,#]
Explanation: Given the above perfect binary tree (Figure A), your function should populate each next pointer to point to its next right node, just like in Figure B. The serialized output is in level order as connected by the next pointers, with '#' signifying the end of each level.
```

Constraints:

- The number of nodes in the given tree is less than 4096.
- -1000 <= node.val <= 1000
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
// Time: O(N) Space: O(1)
class Solution 1 {
public:
    Node* connect(Node* root) {
        if (!root) return root;
        Node* tmp = root, *p = root;
        while(tmp->left != NULL) {
            tmp->left->next = tmp->right;
            if (tmp->next != NULL) {
                tmp->right->next = tmp->next->left;
                tmp = tmp->next;
            } 
            else {
                tmp = p->left;
                p = p->left;
            }
        }
        return root;
    }
};

// Time: O(N), Space: O(N)
class Solution 2 {
public:
    Node* connect(Node* root) {
        queue<Node*> q;
        if (!root) return root;
        q.push(root);
        while(!q.empty()) {
            int len = q.size();
            while(len) {
                Node* cur = q.front();
                q.pop();
                len--;
                if (len && !q.empty()) {
                    cur->next = q.front();
                } else {
                    cur->next = NULL;
                }
                if (cur->left != NULL) q.push(cur->left);
                if (cur->right != NULL) q.push(cur->right);
            }
        }
        return root;
    }
};
```
