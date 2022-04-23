### 1423. Maximum Points You Can Obtain from Cards (Medium)

https://leetcode.com/problems/maximum-points-you-can-obtain-from-cards/

```
// For we can only choose k elements from the head or the end of the vector no matter the order. If we choose i from the head, and we must choose k-i from the end.
// We can first choose all k from the head and replace them with the right elements one by one.
class Solution {
public:
    int maxScore(vector<int>& cardPoints, int k) {
        const int len = cardPoints.size();
        int cur_res = 0;
        for (int i = 0; i < min(k, len); ++i) cur_res += cardPoints[i];
        if (k == len) return cur_res;
        int index = k, res = cur_res;
        while(index--) {
            cur_res = cur_res - cardPoints[index] + cardPoints[len-k+index];
            res = max(res, cur_res);
        }
        return res;
    }
};
```
