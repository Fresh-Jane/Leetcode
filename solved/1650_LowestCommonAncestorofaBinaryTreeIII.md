### 1650. Lowest Common Ancestor of a Binary Tree III (Medium)

https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree-iii/

```
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* left;
    Node* right;
    Node* parent;
};
*/
// Hash table
class Solution {
public:
    Node* lowestCommonAncestor(Node* p, Node * q) {
        unordered_set<Node*> pa;
        while(p) {
            pa.insert(p);
            p = p->parent;
        }
        while(q) {
            if (pa.count(q)) return q;
            q = q->parent;
        }
        return NULL;
    }
};

// Two Pointer
// D(LCA) = A, D(P) = P, D(Q) = Q
// Both of nodes traverse the path with distance (P + A + Q) and meet at LCA.
class Solution {
public:
    Node* lowestCommonAncestor(Node* p, Node * q) {
        Node* a = p;
        Node* b = q;
        while(a != b) {
            a = !a ? q : a->parent;
            b = !b ? p : b->parent;
        }
        return a;
    }
};
```
