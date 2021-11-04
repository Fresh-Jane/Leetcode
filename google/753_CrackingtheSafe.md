### 753. Cracking the Safe (Hard)

https://leetcode.com/problems/cracking-the-safe/

```
// https://leetcode.com/problems/cracking-the-safe/discuss/112966/C%2B%2B-greedy-loop-from-backward-with-explaination
class Solution {
public:
    string crackSafe(int n, int k) {
        string res = string(n, '0');
        unordered_set<string> visited;
        visited.insert(res);
        for (int i = 0; i < pow(k, n); ++i) {
            string prev = res.substr(res.size() - n + 1, n - 1);
            for (int j = k-1; j >= 0; --j) {
                string cur = prev + to_string(j);
                if (!visited.count(cur)) {
                    visited.insert(cur);
                    res += to_string(j);
                    break;
                }
            }
        }
        return res;
    }
};
```
