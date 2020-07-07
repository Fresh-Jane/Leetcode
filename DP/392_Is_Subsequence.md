### 392. Is Subsequence

Given a string s and a string t, check if s is subsequence of t.

A subsequence of a string is a new string which is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (ie, "ace" is a subsequence of "abcde" while "aec" is not).

**Follow up:**
If there are lots of incoming S, say S1, S2, ... , Sk where k >= 1B, and you want to check one by one to see if T has its subsequence. In this scenario, how would you change your code?


**Credits:**
Special thanks to @pbrother for adding this problem and creating all test cases.

 

Example 1:

```
Input: s = "abc", t = "ahbgdc"
Output: true
```

Example 2:

```
Input: s = "axc", t = "ahbgdc"
Output: false
```
 
Constraints:

```
0 <= s.length <= 100
0 <= t.length <= 10^4
Both strings consists only of lowercase characters.
```
```
class Solution 1 {
public:
    bool isSubsequence(string s, string t) {
        int i = 0, j = 0;
        int ls = s.size(), lt = t.size();
        if (ls == 0) return true;
        if (lt < ls) return false;
        while(i < ls && j < lt) {
            if (ls - i - 1 > lt - j - 1) return false;
            if (s[i] == t[j]) i++;
            j++;
        }
        return i == ls;
    }
};

class Solution 2 {
public:
    int findNext(vector<int> seq, int k) {
        int l = 0, r = seq.size();
        while(l < r) {
            int m = (l + r) / 2;
            if (seq[m] <= k) {
                l = m + 1;
            } else {
                r = m;
            }
        }
        return l >= seq.size() ? -1 : seq[l];
    }
    
    bool isSubsequence(string s, string t) {
        unordered_map<char, vector<int>> m;
        int ls = s.size();
        int lt = t.size();
        for (int i = 0; i < lt; ++i) {
            if (!m.count(t[i])) m.insert(make_pair(t[i], 0));
            m[t[i]].push_back(i);
        }
        int k = -1;
        for (int i = 0; i < ls; ++i) {
            if (!m.count(s[i])) return false;
            k = findNext(m[s[i]], k);
            if (k < 0 || lt - k < ls -i) return false;
        }
        return true;
    }
};
```