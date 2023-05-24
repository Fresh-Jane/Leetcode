### 19. Remove Nth Node From End of List (Medium)

https://leetcode.com/problems/remove-nth-node-from-end-of-list/description/

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
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        if (!head || n <= 0) return head;
        ListNode dummy(0);
        dummy.next = head;
        ListNode* fast = &dummy;
        while(n--) fast = fast->next;
        ListNode* slow = &dummy;
        while(fast->next) {
            slow = slow->next;
            fast = fast->next;
        }
        slow->next = slow->next->next;
        return dummy.next;
    }
};
```
