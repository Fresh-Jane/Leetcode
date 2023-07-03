### 138. Copy List with Random Pointer (Medium)

https://leetcode.com/problems/copy-list-with-random-pointer/

```
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* next;
    Node* random;
    
    Node(int _val) {
        val = _val;
        next = NULL;
        random = NULL;
    }
};
*/

// Space: O(1)
// Insert each copy for Node_i between Node_i and Node_i+1, then set their random pointer.
// Finally split the link between the original and copy ones. 
class Solution {
public:
    Node* copyRandomList(Node* head) {
        for (Node* cur = head; cur; cur = cur->next->next) {
            Node* nc = new Node(cur->val);
            nc->next = cur->next;
            cur->next = nc;
        }
        for (Node* cur = head; cur; cur = cur->next->next) {
            if (cur->random) cur->next->random = cur->random->next;
        }
        Node dummy(0);
        Node* copy = &dummy;
        for (Node* cur = head; cur; ) {
            copy->next = cur->next;
            copy = copy->next;
            cur->next = cur->next->next;
            cur = cur->next;
        }
        return dummy.next;
    }
};

// hashmap
class Solution {
public:
    Node* copyRandomList(Node* head) {
        unordered_map<Node*, Node*> m;
        Node dummy(0);
        Node* pre = &dummy;
        Node* cur = head;
        while(cur) {
            Node* new_node = new Node(cur->val);
            pre->next = new_node;
            m[cur] = new_node;
            cur = cur->next;
            pre = new_node;
        }
        cur = head;
        pre = dummy.next;
        while(cur) {
            if (cur->random) {
                pre->random = m[cur->random];
            }
            cur = cur->next;
            pre = pre->next;
        }
        return dummy.next;
    }
};

// Hashmap + DFS
// Space: O(N)
class Solution {
public:
    Node* copyRandomList(Node* head) {
        unordered_map<Node*, Node*> copied;
        return dfs(head, copied);
    }
    Node* dfs(Node* head, unordered_map<Node*, Node*>& copied) {
        if (!head) return head;
        if (copied.count(head)) return copied[head];
        Node* newH = new Node(head->val);
        copied[head] = newH;
        newH->next = dfs(head->next, copied);
        newH->random = dfs(head->random, copied);
        return newH;
    }
};
```
