### 274. H-Index (Medium)

https://leetcode.com/problems/h-index/

```
// Time: O(nlogn), space: O(1)
class Solution {
public:
    int hIndex(vector<int>& citations) {
        if (citations.empty()) return 0;
        sort(citations.begin(), citations.end(), greater<int>());
        int n = citations.size();
        for (int i = 0; i < n; ++i) if (citations[i] < i+1) return i;
        return n;
    }
};
```
