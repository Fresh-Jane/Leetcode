### 148. Sort List (Medium)

https://leetcode.com/problems/sort-list/description/

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
    ListNode* sortList(ListNode* head) {
        if (!head || !head->next) return head;
        ListNode *fast = head, *slow = head;
        while(fast->next && fast->next->next) { // important
            fast = fast->next->next;
            slow = slow->next;
        }
        fast = slow->next;
        slow->next = nullptr;
        ListNode* left = sortList(head);
        ListNode* right = sortList(fast);
        return mergeList(left, right);
    }
    ListNode* mergeList(ListNode* l1, ListNode* l2) {
        if (!l1) return l2;
        if (!l2) return l1;
        if (l1->val < l2->val) {
            l1->next = mergeList(l1->next, l2);
            return l1;
        } else {
            l2->next = mergeList(l2->next, l1);
            return l2;
        }
    }
};
```
