### 528. Random Pick with Weight (Medium)

https://leetcode.com/problems/random-pick-with-weight/

```
class Solution {
public:
    Solution(vector<int>& w) {
        pre_w = w;
        for(int i = 1; i < w.size(); ++i) pre_w[i] += pre_w[i-1];
    }
    
    int pickIndex() {
        int cur = rand() % pre_w.back() + 1;
        return lower_bound(pre_w.begin(), pre_w.end(), cur) - pre_w.begin();
    }
private:
    vector<int> pre_w;
};

/**
 * Your Solution object will be instantiated and called as such:
 * Solution* obj = new Solution(w);
 * int param_1 = obj->pickIndex();
 */
```
