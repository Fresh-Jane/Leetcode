### 142. Linked List Cycle II (Medium)

https://leetcode.com/problems/linked-list-cycle-ii/description/

```
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */

// -------a-------|------b----|-------c--------
//                A           B
// fast and slow first met at B, and then set fast to head, they will neet at A
// (a + b) * 2 = a + b + c + b
//  a = c

class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        if (!head) return head;
        ListNode* slow = head, *fast = head;
        while(fast && fast->next) {
            slow = slow->next;
            fast = fast->next->next;
            if (slow == fast) {
                fast = head;
                while(fast != slow) {
                    fast = fast->next;
                    slow = slow->next;
                }
                return slow;
            }
        }
        return nullptr;
    }
};
```
