### 45. Jump Game II (Medium)

https://leetcode.com/problems/jump-game-ii/

```
// BFS
class Solution {
public:
    int jump(vector<int>& nums) {
        const int n = nums.size();
        if (n == 1) return 0;
        vector<bool> visited(n, false);
        queue<int> q;
        q.push(0);
        visited[0] = true;
        int res = 0;
        while(!q.empty()) {
            int len = q.size();
            while(len--) {
                int cur = q.front();
                q.pop();
                for (int i = cur + 1; i <= min(cur + nums[cur], n - 1); ++i) 
                    if (!visited[i]) {
                        if (i == n - 1) return res + 1;
                        q.push(i);
                        visited[i] = true;
                    }
            }
            res++;
        }
        return res;
    }
};

// Greedy
class Solution {
public:
    int jump(vector<int>& nums) {
        int max_end = 0, end = 0;
        int res = 0;
        for (int i = 0; i < nums.size(); ++i) {
            if (i > end) {
                end = max_end;
                ++res;
            }
            max_end = max(max_end, i + nums[i]);
        }
        return res;
    }
};
```
