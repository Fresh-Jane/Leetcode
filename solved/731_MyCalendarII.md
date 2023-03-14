### 731. My Calendar II (Medium)

https://leetcode.com/problems/my-calendar-ii/description/

```
// O(n)
// The same as https://leetcode.com/problems/my-calendar-iii/description/
class MyCalendarTwo {
public:
    MyCalendarTwo() {}
    
    bool book(int start, int end) {
        int cur = 0;
        ++m[start];
        --m[end];
        for (auto p : m) {
            cur += p.second;
            if (cur >= 3) {
                --m[start];
                ++m[end];
                return false;
            }
        }
        return true;
    }
private:
    map<int, int> m;
};

/**
 * Your MyCalendarTwo object will be instantiated and called as such:
 * MyCalendarTwo* obj = new MyCalendarTwo();
 * bool param_1 = obj->book(start,end);
 */
```
