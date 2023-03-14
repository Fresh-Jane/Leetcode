### 234. Palindrome Linked List (Easy)

https://leetcode.com/problems/palindrome-linked-list/

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
// Solution 1: Recursive
class Solution {
public:
    bool isPalindrome(ListNode* head) {
        if (!head) return true;
        ListNode* slow = head, *fast = head;
        while(fast->next && fast->next->next) {
            slow = slow->next;
            fast = fast->next->next;
        }
        ListNode* second = slow->next;
        second = reverseList(second);
        while(second) {
            if (head->val != second->val) return false;
            head = head->next;
            second = second->next;
        }
        return true;
    }
    ListNode* reverseList(ListNode* head) {
        if (!head || !head->next) return head;
        ListNode* newhead = reverseList(head->next);
        head->next->next = head;
        head->next = NULL;
        return newhead;
    }
};

// Solution 2: Iterative
class Solution {
public:
    bool isPalindrome(ListNode* head) {
        vector<int> nn;
        while(head) {
            nn.push_back(head->val);
            head = head->next;
        }
        int i = 0, j = nn.size() - 1;
        while(i < j) {
            if (nn[i] != nn[j]) return false;
            i++;
            j--;
        }
        return true;
    }
};
```
