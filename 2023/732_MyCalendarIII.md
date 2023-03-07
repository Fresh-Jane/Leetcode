### 732. My Calendar III (Hard)

https://leetcode.com/problems/my-calendar-iii/description/

```
// O(n)
class MyCalendarThree {
public:
    MyCalendarThree() {}
    
    int book(int startTime, int endTime) {
        int cur = 0, res = 0;
        ++m[startTime];
        --m[endTime];
        for (auto p : m) res = max(res, cur += p.second);
        return res;
    }
private:
    map<int, int> m;
};

/**
 * Your MyCalendarThree object will be instantiated and called as such:
 * MyCalendarThree* obj = new MyCalendarThree();
 * int param_1 = obj->book(startTime,endTime);
 */
```
