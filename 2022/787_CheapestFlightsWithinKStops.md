### 787. Cheapest Flights Within K Stops (Medium)

https://leetcode.com/problems/cheapest-flights-within-k-stops/

```
// https://leetcode.com/problems/cheapest-flights-within-k-stops/discuss/115541/JavaC%2B%2BPython-Priority-Queue-Solution-(TLE-now)
// Time: O(VlogV + ElogV)
typedef tuple<int,int,int> ti;
class Solution {
public:
    int findCheapestPrice(int n, vector<vector<int>>& flights, int src, int dst, int K) {
        vector<vector<pair<int,int>>>vp(n);
        for(const auto&f:flights)   vp[f[0]].emplace_back(f[1],f[2]);
        priority_queue<ti,vector<ti>,greater<ti>>pq;
        pq.emplace(0,src,K+1);
        while(!pq.empty()){
            auto [cost,u,stops] = pq.top();
            pq.pop();
            if(u==dst)  return cost;
            if(!stops)  continue;
            for(auto to:vp[u]){
                auto [v,w] = to;
                pq.emplace(cost+w,v,stops-1);
            }
        }
        return -1;
    }
};
```
