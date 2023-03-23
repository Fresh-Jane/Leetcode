### 11. Container With Most Water (Medium)

https://leetcode.com/problems/container-with-most-water/description/

```
class Solution {
public:
    int maxArea(vector<int>& height) {
        const int n = height.size();
        if (n < 2) return 0;
        int i = 0, j = n - 1;
        int res = 0;
        while (i < j) {
            const int min_index = height[i] < height[j] ? i : j;
            res = max(res, height[min_index] * (j - i));
            if (i == min_index) i++;
            else j--;
        }
        return res;
    }
};
```
