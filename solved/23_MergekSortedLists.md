### 23. Merge k Sorted Lists (Hard)

https://leetcode.com/problems/merge-k-sorted-lists/description/

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
    struct Lcmp {
        bool operator() (const ListNode* l1, const ListNode* l2) {
            return l1->val > l2->val;
        }
    };
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        ListNode dummy;
        ListNode* cur = &dummy;
        priority_queue<ListNode*, vector<ListNode*>, Lcmp> pq;
        for (ListNode* node : lists) if (node) pq.push(node);
        while(!pq.empty()) {
            ListNode* node = pq.top(); pq.pop();
            cur->next = node;
            cur = cur->next;
            if (node->next) pq.push(node->next);
        }
        return dummy.next;
    }
};
```
