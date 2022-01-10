### 528. Random Pick with Weight (Medium)

https://leetcode.com/problems/random-pick-with-weight/

```
class Solution {
public:
    Solution(vector<int>& w) {
        pre = w;
        partial_sum(pre.begin(), pre.end(), pre.begin());
    }
    
    int pickIndex() {
        const double r = rand() % pre.back() + 1;
        return lower_bound(pre.begin(), pre.end(), r) - pre.begin();
    }
private:
    vector<int> pre;
};

/**
 * Your Solution object will be instantiated and called as such:
 * Solution* obj = new Solution(w);
 * int param_1 = obj->pickIndex();
 */
```
