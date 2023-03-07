### 729. My Calendar I (Medium)

https://leetcode.com/problems/my-calendar-i/description/ 

```
// BST
// O(logn)
class MyCalendar {
public:
    MyCalendar() {}
    
    bool book(int start, int end) {
        auto it = m.upper_bound(start);
        if (it != m.begin() && prev(it)->second > start) return false;
        if (it != m.end() && it->first < end) return false;
        m[start] = end;
        return true;
    }
private:
    map<int, int> m;
};

/**
 * Your MyCalendar object will be instantiated and called as such:
 * MyCalendar* obj = new MyCalendar();
 * bool param_1 = obj->book(start,end);
 */
```
