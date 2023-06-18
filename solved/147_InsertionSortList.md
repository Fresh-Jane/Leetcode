### 147. Insertion Sort List (Medium)

https://leetcode.com/problems/insertion-sort-list/description/

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
    ListNode* insertionSortList(ListNode* head) {
        if (!head) return head;
        ListNode dummy(0);
        dummy.next = head;
        ListNode* pre = head;
        ListNode* cur = head->next;
        while(cur) {
            if (cur->val >= pre->val) {
                pre = cur;
                cur = cur->next;
            } else {
                pre->next = cur->next;
                ListNode* p = &dummy;
                while(cur->val >= p->next->val) p = p->next;
                cur->next = p->next;
                p->next = cur;
                cur = pre->next;
            }
        }
        return dummy.next;
    }
};
```
