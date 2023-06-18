### 92. Reverse Linked List II (Medium)

https://leetcode.com/problems/reverse-linked-list-ii/description/

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
class Solution {
public:
    ListNode* reverseBetween(ListNode* head, int left, int right) {
        if (!head || !head->next || left == right) return head;
        ListNode dummy(0);
        dummy.next = head;
        ListNode* p = &dummy;
        int l = right - left + 1;
        while(--left) p = p->next;
        ListNode* tail = p->next;

        ListNode* cur = tail;
        ListNode* pre = NULL;
        while(l--) {
            ListNode* next = cur->next;
            cur->next = pre;
            pre = cur;
            cur = next;
        } 

        tail->next = cur;
        p->next = pre;
        return dummy.next;
    }
};
```
