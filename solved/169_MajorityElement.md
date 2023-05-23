### 169. Majority Element (Easy)

https://leetcode.com/problems/majority-element/description/

```
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int res = 0, votes = 0;
        for (int num : nums) {
            if (num == res) ++votes;
            else {
                if (votes == 0) res = num, votes = 1;
                else --votes;
            }
        }
        return res;
    }
};
```
