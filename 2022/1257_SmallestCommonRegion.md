### 1257. Smallest Common Region (Medium)

https://leetcode.com/problems/smallest-common-region/

```
class Solution {
public:
    string findSmallestRegion(vector<vector<string>>& regions, string region1, string region2) {
        unordered_map<string, string> m;
        vector<string> pre1, pre2;
        for (auto region : regions) 
            for (int i = 1; i < region.size(); ++i)
                m[region[i]] = region[0];
        while(!region1.empty()) {
            pre1.push_back(region1);
            region1 = m[region1];
        }
        while(!region2.empty()) {
            pre2.push_back(region2);
            region2 = m[region2];
        }
        for (auto p1 : pre1) 
            for (auto p2 : pre2)
                if (p1 == p2)
                    return p1;
        return "";
    }
};
```
