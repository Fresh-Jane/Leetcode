### 1802. Maximum Value at a Given Index in a Bounded Array (Medium)

https://leetcode.com/problems/maximum-value-at-a-given-index-in-a-bounded-array/description/

```
// Binary search
// search max value and can O(1) get left and right sum
class Solution {
public:
    using ll = long long;
    ll cal(ll n) {
        return (n * (n+1)) / 2;
    }
    ll getSum(int cnt, int max_num) {
        if (cnt >= max_num) return cal(max_num) + cnt - max_num;
        else return cal(max_num) - cal(max_num - cnt);
    }
    int maxValue(int n, int index, int maxSum) {
        int leftCnt = index, rightCnt = n - index - 1;
        int l = 1, r = maxSum;
        int res = -1;
        while(l <= r) {
            int mid = l + (r - l) / 2;
            ll leftSum = getSum(leftCnt, mid-1);
            ll rightSum = getSum(rightCnt, mid-1);
            ll sum = leftSum + mid + rightSum;
            if (sum > maxSum) r = mid - 1;
            else {
                res = mid;
                l = mid + 1;
            }
        }
        return res;
    }
};
```
