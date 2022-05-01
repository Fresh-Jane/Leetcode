### 1011. Capacity To Ship Packages Within D Days (Medium)

https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/

```
// Binary search
// The search range is from the max elements in the array to the sum of array.
// Verify if we can ship the weights with given max capacity
class Solution {
public:
    int shipWithinDays(vector<int>& weights, int days) {
        int left = 0, right = 0;
        for (int w : weights) {
            left = max(left, w);
            right += w;
        }
        while(left < right) {
            int mid = left + (right - left) / 2;
            if (can(weights, mid, days)) right = mid;
            else left = mid + 1;
        }
        return left;
    }
    bool can(vector<int>& weights, int cap, int days) {
        int d = 1, sum = 0;
        for (int w : weights) {
            if (sum + w <= cap) sum += w;
            else {
                sum = w;
                ++d;
            }
            if (d > days) return false;
        }
        return true;
    }
};
```
