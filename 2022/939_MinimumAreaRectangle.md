### 939. Minimum Area Rectangle (Medium)

https://leetcode.com/problems/minimum-area-rectangle/

```
// Use unordered_set and re-impelement the hash function
class Solution {
public:
    struct P {
        int x,y;
    };
    struct pHash {
        size_t operator()(const P& p1) const {
            return hash<int>{}(p1.x) ^ hash<int>{}(p1.y);
        }  
    };
    struct pEqual {
        bool operator()(const P& p1, const P& p2) const {
            return p1.x == p2.x && p1.y == p2.y;
        }  
    };
    int minAreaRect(vector<vector<int>>& points) {
        const int n = points.size();
        unordered_set<P, pHash, pEqual> s(n, pHash(), pEqual());
        int res = INT_MAX;
        for (int i = 0; i < n; ++i) s.insert({points[i][0], points[i][1]});
        for (int i = 0; i < n; ++i) {
            const int x1 = points[i][0], y1 = points[i][1];
            for (int j = 0; j < n; ++j) {
                if (j == i) continue;
                const int x3 = points[j][0], y3 = points[j][1];
                if (x3 == x1 || y3 == y1) continue;
                const P p2({x1, y3}), p4({x3, y1});
                if (s.count(p2) && s.count(p4)) res = min(res, abs(x3-x1)*abs(y3-y1));
            }
        }
        return res == INT_MAX ? 0 : res;
    }
};

// Use unordered_map 
class Solution {
public:
    int minAreaRect(vector<vector<int>>& points) {
        const int n = points.size();
        unordered_map<int, unordered_set<int>> s;
        int res = INT_MAX;
        for (int i = 0; i < n; ++i) s[points[i][0]].insert(points[i][1]);
        for (int i = 0; i < n; ++i) {
            const int x1 = points[i][0], y1 = points[i][1];
            for (int j = 0; j < n; ++j) {
                if (j == i) continue;
                const int x3 = points[j][0], y3 = points[j][1];
                if (x3 == x1 || y3 == y1) continue;
                if (s[x1].count(y3) && s[x3].count(y1)) res = min(res, abs(x3-x1)*abs(y3-y1));
            }
        }
        return res == INT_MAX ? 0 : res;
    }
};
```
