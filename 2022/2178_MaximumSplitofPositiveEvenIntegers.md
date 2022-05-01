### 2178. Maximum Split of Positive Even Integers (Medium)

https://leetcode.com/problems/maximum-split-of-positive-even-integers/

```
class Solution {
public:
    vector<long long> maximumEvenSplit(long long finalSum) {
        vector<long long> res;
        if (finalSum % 2) return res;
        long long i = 2;
        while(finalSum > i * 2) {
            res.push_back(i);
            finalSum -= i;
            i += 2;
        }
        res.push_back(finalSum);
        return res;
    }
};
```
