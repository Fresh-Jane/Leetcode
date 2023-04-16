### 3. Longest Substring Without Repeating Characters (Medium)

https://leetcode.com/problems/longest-substring-without-repeating-characters/

```
// Hashmap + two pointer
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        unordered_set<char> st;
        int l = 0, r = 0;
        int res = 0;
        while(l <= r && r < s.size()) {
            if (!st.count(s[r])) {
                st.insert(s[r]);
                r++;
            } else {
                res = max(res, r - l);
                while(st.count(s[r])) {
                    st.erase(s[l]);
                    l++;
                }
            }
        }
        return max(res, r - l);
    }
};

class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        unordered_map<char, int> cnt;
        int l = 0, r = 0;
        const int n = s.size();
        int res = 0;
        while(r < n) {
            cnt[s[r]]++;
            while (cnt[s[r]] > 1 && l < r) {
                cnt[s[l]]--;
                l++;
            }
            res = max(res, r - l + 1);
            r++;
        }
        return res;
    }
};
```
