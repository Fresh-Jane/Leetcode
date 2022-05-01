### 253. Meeting Rooms II (Medium)

https://leetcode.com/problems/meeting-rooms-ii/

```
// Greedy
// The new meeting should open one new meeting room if there is no previous meeting ends before it.
class Solution {
public:
    int minMeetingRooms(vector<vector<int>>& intervals) {
        sort(intervals.begin(), intervals.end(),
            [](const vector<int>& i1, const vector<int>& i2) {
                if (i1[0] == i2[0]) return i1[1] < i2[1];
                return i1[0] < i2[0];
            });
        priority_queue<int, vector<int>, greater<int>> pq;
        for (const auto& inter : intervals) {
            if (!pq.empty() && inter[0] >= pq.top()) pq.pop();
            pq.push(inter[1]);
        }
        return pq.size();
    }
};

// Similar to 732-MyCalendarIII
class Solution {
public:
    int minMeetingRooms(vector<vector<int>>& intervals) {
        map<int, int> m;
        for (const vector<int>& i : intervals) {
            m[i[0]]++;
            m[i[1]]--;
        }
        int cur = 0, res = 0;
        for (auto it : m) 
            res = max(res, cur += it.second);
        return res;
    }
};
```
