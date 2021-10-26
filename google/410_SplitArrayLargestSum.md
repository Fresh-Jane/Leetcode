### 410. Split Array Largest Sum (Hard)

https://leetcode.com/problems/split-array-largest-sum/

```
Ref: https://leetcode.com/problems/split-array-largest-sum/discuss/89819/C%2B%2B-Fast-Very-clear-explanation-Clean-Code-Solution-with-Greedy-Algorithm-and-Binary-Search

Binary search the max sum.

class Solution {
public:
    bool doable(const vector<int>& nums, int cut, long long max) {
        long long acc = 0;
        for (const int num : nums) {
            if (num > max) return false;
            else if (acc + num <= max) acc += num;
            else {
                --cut;
                acc = num;
                if (cut < 0) return false;
            }
        }
        return true;
    }
    
    int splitArray(vector<int>& nums, int m) {
        long long l = 0, r = 0;
        for (const int num : nums) {
            l = max(l, (long long)num);
            r += num;
        }
        while (l < r) {
            long long mid = l + (r - l) / 2;
            if (doable(nums, m - 1, mid)) r = mid;
            else l = mid + 1;
        }
        return l;
    }
};
```
