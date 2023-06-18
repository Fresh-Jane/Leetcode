### 24. Swap Nodes in Pairs (Medium)

https://leetcode.com/problems/swap-nodes-in-pairs/description/

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
    ListNode* swapPairs(ListNode* head) {
        if (!head || !head->next) return head;
        ListNode dummy(0);
        ListNode* pre = &dummy;
        ListNode* cur = head;
        while(cur && cur->next) {
            ListNode* next = cur->next;
            cur->next = next->next;
            next->next = cur;
            pre->next = next;
            pre = cur;
            cur = cur->next;
        }
        return dummy.next;
    }
};
```
