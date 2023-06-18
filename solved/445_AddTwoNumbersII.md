### 445. Add Two Numbers II (Medium)

https://leetcode.com/problems/add-two-numbers-ii/description/

```
// Reverse
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
    ListNode* reverseList(ListNode* l) {
        ListNode* pre = NULL;
        while(l) {
            ListNode* next = l->next;
            l->next = pre;
            pre = l;
            l = next;
        }
        return pre;
    }

    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode* rl1 = reverseList(l1);
        ListNode* rl2 = reverseList(l2);
        ListNode dummy(0);
        ListNode* head = &dummy;
        for (int carry = 0; rl1 || rl2 || carry; carry /= 10) {
            if (rl1) { carry += rl1->val; rl1 = rl1->next; }
            if (rl2) { carry += rl2->val; rl2 = rl2->next; }
            head->next = new ListNode(carry % 10);
            head = head->next;
        }
        return reverseList(dummy.next);
    }
};

// No reverse
// Use stack
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
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        if (!l1) return l2;
        if (!l2) return l1;
        stack<int> s1, s2;
        while(l1) { s1.push(l1->val); l1 = l1->next; }
        while(l2) { s2.push(l2->val); l2 = l2->next; }
        ListNode* cur = NULL;
        int carry = 0;
        for (int carry = 0; !s1.empty() || !s2.empty() || carry; carry /= 10) {
            if (!s1.empty()) { carry += s1.top(); s1.pop(); }
            if (!s2.empty()) { carry += s2.top(); s2.pop(); }
            ListNode* pre = new ListNode(carry % 10);
            pre->next = cur;
            cur = pre;
        }
        return cur;
    }
};

```
