### 2187. Minimum Time to Complete Trips (Medium)

https://leetcode.com/problems/minimum-time-to-complete-trips/description/

```
// Binary search
class Solution {
public:
    long long minimumTime(vector<int>& time, int totalTrips) {
        int min_t = INT_MAX;
        for (const int t : time) min_t = min(min_t, t);
        long long l = 1, r = (long long)min_t * totalTrips;
        while(l < r) {
            long long m = l + (r - l) / 2;
            if (can(time, m, totalTrips)) r = m;
            else l = m + 1;
        }
        return l;
    }
    bool can(const vector<int>& time, long long total_time, int totalTrips) {
        int trips = 0;
        for (const int t : time) {
            trips += total_time / t;
            if (trips >= totalTrips) return true;
        }
        return false;
    }
};
```
