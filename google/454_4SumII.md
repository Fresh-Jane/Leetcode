### 454. 4Sum II (Medium)

https://leetcode.com/problems/4sum-ii/

```
// Split the array lists into 2 group, add sum and record as map in each group. Search the minus sum in another group.
class Solution {
public:
    int fourSumCount(vector<int>& nums1, vector<int>& nums2, vector<int>& nums3, vector<int>& nums4) {
        vector<vector<int>> lists({nums1, nums2, nums3, nums4});
        return kSumCount(lists);
    }
    int kSumCount(const vector<vector<int>>& lists) {
        unordered_map<int, int> m;
        addHash(lists, m, 0, 0);
        return count(lists, m, lists.size() / 2, 0);
    }
    void addHash(const vector<vector<int>>& lists, unordered_map<int, int>& m, int i, int sum) {
        if (i == lists.size() / 2) 
            ++m[sum];
        else 
            for (int a : lists[i])
                addHash(lists, m, i + 1, sum + a);
    }
    int count(const vector<vector<int>>& lists, const unordered_map<int, int>& m, int i, int c) {
        if (i == lists.size()) {
            auto it = m.find(c);
            return it == m.end() ? 0 : m.at(c);
        }
        int cnt = 0;
        for (int a : lists[i]) 
            cnt += count(lists, m, i + 1, c - a);
        return cnt;
    }
};
```
