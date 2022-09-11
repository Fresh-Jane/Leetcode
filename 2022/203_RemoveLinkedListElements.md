### 203. Remove Linked List Elements (Easy)

https://leetcode.com/problems/remove-linked-list-elements/

```
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */

// Recursive
class Solution {
public:
    ListNode* removeElements(ListNode* head, int val) {
        if (!head) return head;
        head->next = removeElements(head->next, val);
        return head->val != val ? head : head->next;
    }
};

// Iterative
class Solution {
public:
    ListNode* removeElements(ListNode* head, int val) {
        if (!head) return head;
        ListNode dummy;
        ListNode* cur = &dummy;
        while(head) {
            if (head->val != val) {
                cur->next = head;
                cur = cur->next;
            }
            head = head->next;
        }
        cur->next = NULL;
        return dummy.next;
    }
};
```
