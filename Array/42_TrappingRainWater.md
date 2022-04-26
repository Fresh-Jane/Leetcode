### 42. Trapping Rain Water (Hard)

https://leetcode.com/problems/trapping-rain-water/

```
// Two pointer
// For we always move the side with smaller height, so the other side with higher height, we use the same side max minus current lower height.
class Solution {
public:
    int trap(vector<int>& height) {
        int l = 0, r = height.size() - 1;
        int lmax = 0, rmax = 0;
        int res = 0;
        while(l <= r) {
            if (height[l] < height[r]) {
                if (height[l] >= lmax) lmax = height[l];
                else res += lmax - height[l];
                ++l;
            } else {
                if (height[r] >= rmax) rmax = height[r];
                else res += rmax - height[r];
                --r;
            }
        }
        return res;
    }
};
```
