### 1822. Sign of the Product of an Array (Easy)

https://leetcode.com/problems/sign-of-the-product-of-an-array/

```
class Solution {
public:
    int arraySign(vector<int>& nums) {
        int neg_num = 0;
        for (int num : nums) {
            if (num == 0) return 0;
            if (num < 0) ++neg_num;
        }
        return neg_num % 2 ? -1 : 1;
    }
};
```
