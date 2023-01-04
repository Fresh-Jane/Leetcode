### 1863. Sum of All Subset XOR Totals (Easy)

https://leetcode.com/problems/sum-of-all-subset-xor-totals/

```
// https://leetcode.com/problems/sum-of-all-subset-xor-totals/discuss/1211067/C%2B%2B-Simple-approach-with-Explanation
class Solution {
public:
    int subsetXORSum(vector<int>& nums) {
        int cnt = nums.size();
        int numSubSets = pow(2, cnt);
        int res = 0;
        for (int i = 1; i < numSubSets; ++i) {
            int curXOR = 0;
            for (int j = 0, bit = i; j < cnt; ++j, bit >>= 1)
                if (bit & 1)
                    curXOR ^= nums[j];
            res += curXOR;
        }
        return res;
    }
};
```
