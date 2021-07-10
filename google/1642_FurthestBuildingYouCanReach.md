### 1642. Furthest Building You Can Reach (Medium)

https://leetcode.com/problems/furthest-building-you-can-reach/

```
class Solution {
public:
    int furthestBuilding(vector<int>& heights, int bricks, int ladders) {
        priority_queue<int, vector<int>, greater<int>> q;
        const int n = heights.size();
        for (int i = 1; i < n; ++i) {
            const int diff = heights[i] - heights[i-1];
            if (diff <= 0) continue;
            q.push(diff);
            if (q.size() > ladders) {
                const int now = q.top(); q.pop();
                if (bricks < now) return i - 1;
                bricks -= now;
            }
        }
        return n - 1;
    }
};
```
