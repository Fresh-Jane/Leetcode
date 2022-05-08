### 708. Insert into a Sorted Circular Linked List (Medium)

https://leetcode.com/problems/insert-into-a-sorted-circular-linked-list/

```
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* next;

    Node() {}

    Node(int _val) {
        val = _val;
        next = NULL;
    }

    Node(int _val, Node* _next) {
        val = _val;
        next = _next;
    }
};
*/

class Solution {
public:
    Node* insert(Node* head, int v) {
        Node* newN = new Node(v);
        if (!head) {
            newN->next = newN;
            return newN;
        }
        Node* cur = head;
        while(cur->next != head) {
            int cv = cur->val, nv = cur->next->val;
            if (cv <= v && v <= nv) break;
            if (cv > nv && (cv <= v || v <= nv)) break;
            cur = cur->next;
        }
        newN->next = cur->next;
        cur->next = newN;
        return head;
    }
};
```
