### 1710. Maximum Units on a Truck (Easy)

https://leetcode.com/problems/maximum-units-on-a-truck/

```
class Solution {
public:
    int maximumUnits(vector<vector<int>>& boxTypes, int truckSize) {
        sort(boxTypes.begin(), boxTypes.end(), 
            [](const vector<int>& b1, const vector<int>& b2){
                return b1[1] > b2[1];
            });
        int unit_num = 0;
        for (auto box : boxTypes) {
            int cur = truckSize >= box[0] ? box[0] : truckSize;
            unit_num += box[1] * cur;
            truckSize -= cur;
            if (!truckSize) break;
        }
        return unit_num;
    }
};
```
