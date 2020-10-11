### 743. Network Delay Time (Medium)

There are N network nodes, labelled 1 to N.

Given times, a list of travel times as directed edges times[i] = (u, v, w), where u is the source node, v is the target node, and w is the time it takes for a signal to travel from source to target.

Now, we send a signal from a certain node K. How long will it take for all nodes to receive the signal? If it is impossible, return -1.

Example 1:

```
Input: times = [[2,1,1],[2,3,1],[3,4,1]], N = 4, K = 2
Output: 2
```

Note:

- N will be in the range [1, 100].
- K will be in the range [1, N].
- The length of times will be in the range [1, 6000].
- All edges times[i] = (u, v, w) will have 1 <= u, v <= N and 0 <= w <= 100.

```
// Shortest path in directed graph from single source
// Dijkstra
class Solution {
public:  
    int networkDelayTime(vector<vector<int>>& times, int N, int K) {
        vector<vector<int>> tmap(N+1, vector<int>(N+1, INT_MAX));
        for (int i = 0; i < (int)times.size(); ++i) 
            tmap[times[i][0]][times[i][1]] = times[i][2];
        vector<int> time(N+1, INT_MAX);
        vector<bool> visit(N+1, false);
        time[K] = 0;
        for (int i = 1; i <= N; ++i) {
            int min_res = INT_MAX, k;
            for (int j = 1; j <= N; ++j) {
                if (!visit[j] && time[j] < min_res) {
                    min_res = time[j];
                    k = j;
                }
            }
            visit[k] = true;
            for (int j = 1; j <= N; ++j) {
                if (!visit[j] && tmap[k][j] < INT_MAX) {
                    time[j] = min(time[j], time[k] + tmap[k][j]);
                }
            }
        }
        int res = 0;
        for (int i = 1; i <= N; ++i) {
            if (time[i] == INT_MAX) return -1;
            res = max(res, time[i]);
        }
        return res;
    }
};

```
