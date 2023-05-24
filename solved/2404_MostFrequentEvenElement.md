### 2404. Most Frequent Even Element (Easy)

https://leetcode.com/problems/most-frequent-even-element/description/

```
class Solution {
public:
    int mostFrequentEven(vector<int>& nums) {
        map<int, int> fre_even;
        for (int num : nums) 
            if (num % 2 == 0) fre_even[num]++;
        int max_num = 0;
        int res = -1;
        for (const auto& pair : fre_even) 
            if (pair.second > max_num) {
                res = pair.first;
                max_num = pair.second;
            }
        return res;
    }
};
```
