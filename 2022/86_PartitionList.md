### 86. Partition List (Medium)

https://leetcode.com/problems/partition-list/

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

// Use two dummy node to lead two list for one contains elements smaller than x, another one contains larger elements.
// Then merge two list.
// Time: O(N)
// Space: O(1)
class Solution {
public:
    ListNode* partition(ListNode* head, int x) {
        ListNode small_dummy(0);
        ListNode* small = &small_dummy;
        ListNode large_dummy(0);
        ListNode* large = &large_dummy;
        for(ListNode* cur = head; cur; cur = cur->next) {
            if (cur->val < x) {
                small->next = cur;
                small = small->next;
            } else {
                large->next = cur;
                large = large->next;
            }
        }
        small->next = large_dummy.next;
        large->next = nullptr;
        return small_dummy.next;
    }
};
```
