### 1345. Jump Game IV (Hard)

https://leetcode.com/problems/jump-game-iv/

```
class Solution {
public:
    int minJumps(vector<int>& arr) {
        const int len = arr.size();
        if (len < 2) return 0;
        // dedup, allow at most 2 consecutive equal numbers
        int n = 2;
        for (int i = 2; i < len; ++i) 
            if (arr[i] != arr[i-1] || arr[i] != arr[i-2]) arr[n++] = arr[i];
        arr.resize(n);
        unordered_map<int, vector<int>> m;
        vector<bool> dp(n, false);
        for (int i = 0; i < n; ++i) m[arr[i]].push_back(i);
        queue<int> q;
        int res = 0;
        q.push(0);
        dp[0] = true;
        while (!q.empty()) {
            const int size = q.size();
            for (int i = 0; i < size; ++i) {
                int cur = q.front();
                q.pop();
                if (cur == n - 1) return res;
                dp[cur] = true;
                for (int n_cur : m[arr[cur]]) 
                    if (!dp[n_cur]) q.push(n_cur);
                if (cur + 1 < n && !dp[cur+1]) q.push(cur+1);
                if (cur - 1 >= 0 && !dp[cur-1]) q.push(cur-1);
            }
            res++;
        }
        return res;    
    }
};
```
