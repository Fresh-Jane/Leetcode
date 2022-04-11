### 815. Bus Routes (Hard)

https://leetcode.com/problems/bus-routes/

```
// Self. BFS
class Solution {
public:
    int numBusesToDestination(vector<vector<int>>& routes, int source, int target) {
        if (target == source) return 0;
        unordered_map<int, vector<int>> m;
        for (int i = 0; i < routes.size(); ++i) 
            for (const int r : routes[i]) m[r].push_back(i);
        unordered_set<int> visit_s;
        queue<int> q;
        q.push(source);
        visit_s.insert(source);
        int res = 1;
        while(!q.empty()) {
            int len = q.size();
            while(len--) {
                int cur_s = q.front(); q.pop();
                if (cur_s == target) return res;
                for (int bus : m[cur_s]) {
                    for (int stop : routes[bus]) {
                        if (visit_s.count(stop)) continue;
                        if (stop == target) return res;
                        q.push(stop);
                        visit_s.insert(stop);
                    }
                    routes[bus].clear();
                }
            }
            res++;
        }
        return -1;
    }
};
```
