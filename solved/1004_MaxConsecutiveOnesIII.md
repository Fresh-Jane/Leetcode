### 1004. Max Consecutive Ones III (Medium)

https://leetcode.com/problems/max-consecutive-ones-iii/

```
// Slideing window
class Solution {
public:
    int longestOnes(vector<int>& nums, int k) {
        int res = 0;
        for (int i = 0, j = 0; i < nums.size(); ++i) {
            if (nums[i] == 0) --k;
            while(k < 0) 
                if (nums[j++] == 0) ++k;
            res = max(res, i-j+1);
        }
        return res;
    }
};
```
