### 430. Flatten a Multilevel Doubly Linked List (Medium)

https://leetcode.com/problems/flatten-a-multilevel-doubly-linked-list/

```
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* prev;
    Node* next;
    Node* child;
};
*/
// First regard the doubly linked list as one binary tree, which the child pointer is left subtree and next pointer is for the right one.
// Use recursive implementation for the dfs.
// The first node can make the solution more concise and elegant by reducing null pointer checks.
class Solution {
public:
    Node* flatten(Node* head) {
        if (!head) return NULL;
        Node* first = new Node(0, NULL, head, NULL);
        flat(first, head);
        first->next->prev = NULL;
        return first->next;
    }
    Node* flat(Node* pre, Node* cur) {
        if (!cur) return pre;
        cur->prev = pre;
        pre->next = cur;
        Node* next = cur->next; 
        Node* ltail = flat(cur, cur->child);
        cur->child = NULL;
        return flat(ltail, next);
    }
};
```
