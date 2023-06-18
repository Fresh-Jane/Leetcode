### 141. Linked List Cycle (Easy)

https://leetcode.com/problems/linked-list-cycle/description/

```
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */

// Two pointer
// Space: O(1)
class Solution {
public:
    bool hasCycle(ListNode *head) {
        ListNode* fast = head, *slow = head;
        while(fast && fast->next) {
            slow = slow->next;
            fast = fast->next->next;
            if (fast == slow) return true;
        }
        return false;
    }
};

// Change the special val to represent we have visited the node
class Solution {
public:
    bool hasCycle(ListNode *head) {
        while(head) {
            if (head->val == 1000000) return true;
            head->val = 1000000;
            head = head->next;
        }
        return false;
    }
};

// Brote force
// Unordered_set
class Solution {
public:
    bool hasCycle(ListNode *head) {
        unordered_set<ListNode*> s;
        while(head) {
            if (s.count(head)) return true;
            s.insert(head);
            head = head->next;
        }
        return false;
    }
};
```
