### 1386. Cinema Seat Allocation (Medium)

https://leetcode.com/problems/cinema-seat-allocation/

```
class Solution {
public:
    int maxNumberOfFamilies(int n, vector<vector<int>>& reservedSeats) {
        int res = 2 * n;
        unordered_map<int, char> m; // char is 8 bit
        for (auto& s : reservedSeats)
            if (s[1] > 1 && s[1] < 10) m[s[0]] |= 1<<(s[1]-2); // << is bit move
        for (auto& seat : m) {
            bool p1 = !(seat.second & 0b11110000); // 0b is for binary
            bool p2 = !(seat.second & 0b00111100);
            bool p3 = !(seat.second & 0b00001111);
            if (p1 && p3)continue;
            if (p1 || p2 || p3) res -= 1;
            else res -= 2;
        }
        return res;
    }
};
```
