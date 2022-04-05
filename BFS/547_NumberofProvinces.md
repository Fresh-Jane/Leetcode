### 547. Number of Provinces (Medium)

https://leetcode.com/problems/number-of-provinces/

```
class Solution {
public:
    vector<int> pre;
    int count;
    int find(int x) {
        if (pre[x] != x) pre[x] = find(pre[x]);
        return pre[x];
    }
    void link(int x, int y) {
        const int px = find(x), py = find(y);
        if (px != py) {
            pre[py] = px;
            --count;
        }
    }
    int findCircleNum(vector<vector<int>>& isConnected) {
        const int n = isConnected.size();
        pre.resize(n, 0);
        count = n;
        for (int i = 0; i < n; ++i) pre[i] = i;
        for (int i = 0; i < n; ++i) 
            for (int j = 0; j < n; ++j) 
                if (isConnected[i][j]) link(i, j);
        return count;
    }
};
```
