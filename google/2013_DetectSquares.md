### 2013. Detect Squares (Medium)

https://leetcode.com/problems/detect-squares/

```
class DetectSquares {
public:
    void add(vector<int> point) {
        cnt[point[0]][point[1]]++;
        points.push_back({point[0], point[1]});
    }
    
    int count(vector<int> point) {
        const int x = point[0], y = point[1];
        int res = 0;
        for (auto& [x3, y3] : points) {
            if (abs(x3-x) == 0 || abs(y3-y) != abs(x3-x)) continue;
            res += cnt[x][y3] * cnt[x3][y];
        }
        return res;
    }
private:
    int cnt[1001][1001] = {};
    vector<pair<int, int>> points;
};

/**
 * Your DetectSquares object will be instantiated and called as such:
 * DetectSquares* obj = new DetectSquares();
 * obj->add(point);
 * int param_2 = obj->count(point);
 */
```
