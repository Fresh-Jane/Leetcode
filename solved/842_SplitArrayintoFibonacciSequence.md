### 842. Split Array into Fibonacci Sequence (Medium)

https://leetcode.com/problems/split-array-into-fibonacci-sequence/description/

```
class Solution {
public:
    vector<int> splitIntoFibonacci(string num) {
        vector<int> res;
        dfs(num, 0, res);
        return res;
    }
    bool dfs(const string& num, int start, vector<int>& path) {
        if (start == num.size() && path.size() > 2) {
            return true;
        }
        for (int i = 1; i <= 10 && start + i <= num.size(); ++i) {
            const string cur = num.substr(start, i);
            if (i > 1 && cur[0] == '0') break;
            long long cnum = stoll(cur);
            if (cnum > INT_MAX) break;
            if (path.size() < 2 || (long long)path[path.size() - 1] + (long long)path[path.size() - 2] == cnum) {
                path.push_back(cnum);
                if (dfs(num, start + i, path)) return true;
                path.pop_back();
            } else if ((long long)path[path.size() - 1] + (long long)path[path.size() - 2] < cnum) break;
        }
        return false;
    }
};
```
