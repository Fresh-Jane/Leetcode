### 223. Rectangle Area (Medium)

https://leetcode.com/problems/rectangle-area/description/

```
class Solution {
public:
    int computeArea(int ax1, int ay1, int ax2, int ay2, int bx1, int by1, int bx2, int by2) {
        int left = max(ax1, bx1), right = min(ax2, bx2);
        int bottom = max(ay1, by1), top = min(ay2, by2);
        int overlap = (left < right && bottom < top) ? (right - left) * (top - bottom) : 0;
        return (ax2 - ax1) * (ay2 - ay1) + (bx2 - bx1) * (by2 - by1) - overlap;
    }
};
```
