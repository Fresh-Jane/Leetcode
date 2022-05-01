### 1131. Maximum of Absolute Value Expression (Medium)

https://leetcode.com/problems/maximum-of-absolute-value-expression/

ref: 
https://leetcode.com/problems/maximum-of-absolute-value-expression/discuss/340075/c%2B%2B-beats-100-(both-time-and-memory)-with-algorithm-and-image
https://leetcode.com/problems/maximum-of-absolute-value-expression/discuss/339968/JavaC%2B%2BPython-Maximum-Manhattan-Distance
```
class Solution {
public:
    int maxAbsValExpr(vector<int>& arr1, vector<int>& arr2) {
        const int n = arr1.size();
        int smallest, res = 0;
        for (int p : {1, -1}) {
            for (int q : {1, -1}) {
                smallest = p * arr1[0] + q * arr2[0] + 0;
                for (int i = 1; i < n; ++i) {
                    int cur = p * arr1[i] + q * arr2[i] + i;
                    res = max(res, cur - smallest);
                    smallest = min(cur, smallest);
                }
            }
        }
        return res;
    }
};
```
