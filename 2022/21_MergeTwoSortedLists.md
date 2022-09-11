### 21. Merge Two Sorted Lists (Easy)

https://leetcode.com/problems/merge-two-sorted-lists/

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
// Solution 1: Iterative
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
        ListNode dummy;
        ListNode* cur = &dummy;
        while(list1 || list2) {
            if (!list1 || (list1 && list2 && list1->val > list2->val)) {
                cur->next = new ListNode(list2->val);
                list2 = list2->next;
            } else {
                cur->next = new ListNode(list1->val);
                list1 = list1->next;
            }
            cur = cur->next;
        }
        return dummy.next;
    }
};

// Solution 2: Recursive
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
        if (!list1) return list2;
        if (!list2) return list1;
        if (list1->val < list2->val) {
            list1->next = mergeTwoLists(list1->next, list2);
            return list1;
        } else {
            list2->next = mergeTwoLists(list1, list2->next);
            return list2;
        }       
    }
};
```
