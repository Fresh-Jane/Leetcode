### 707. Design Linked List (Medium)

https://leetcode.com/problems/design-linked-list/description/

```
// struct ListNode {
//     int val;
//     ListNode* next;
//     ListNode() : val(0), next(nullptr) {}
//     ListNode(int x) : val(x), next(nullptr) {}
//     ListNode(int x, ListNode* n) : val(x), next(n) {}
// };
class MyLinkedList {
public:
    MyLinkedList() {
        head = new ListNode(0);
        tail = head;
    }

    ListNode* find(int index) {
        ListNode* p = head;
        while(index--) p = p->next;
        return p;
    }
    
    int get(int index) {
        if (index >= size || index < 0) return -1;
        ListNode* pre = find(index);
        return pre->next->val;
    }
    
    void addAtHead(int val) {
        addAtIndex(0, val);
    }
    
    void addAtTail(int val) {
        tail->next = new ListNode(val);
        tail = tail->next;
        size++;
    }
    
    void addAtIndex(int index, int val) {
        if (index > size || index < 0) return;
        if (index == size) { addAtTail(val); return; }
        ListNode* pre = find(index);
        ListNode* pre_next = pre->next;
        pre->next = new ListNode(val, pre_next);
        size++;
    }
    
    void deleteAtIndex(int index) {
        if (index >= size || index < 0) return;
        ListNode* pre = find(index);
        ListNode* pre_next_next = pre->next->next;
        delete(pre->next);
        if (index == size - 1) tail = pre;

        pre->next = pre_next_next;
        size--;
    }
private:
    ListNode* head;
    ListNode* tail;
    int size = 0;
};

/**
 * Your MyLinkedList object will be instantiated and called as such:
 * MyLinkedList* obj = new MyLinkedList();
 * int param_1 = obj->get(index);
 * obj->addAtHead(val);
 * obj->addAtTail(val);
 * obj->addAtIndex(index,val);
 * obj->deleteAtIndex(index);
 */
```
