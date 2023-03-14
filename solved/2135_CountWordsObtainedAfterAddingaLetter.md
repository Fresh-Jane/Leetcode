### 2135. Count Words Obtained After Adding a Letter (Medium)

https://leetcode.com/problems/count-words-obtained-after-adding-a-letter/

```
// Sort the string and use unordered_set to save them.
class Solution {
public:
    int wordCount(vector<string>& startWords, vector<string>& targetWords) {
        unordered_set<int> m;
        for (string s : startWords) {
            long h = 0;
            for (int i = 0; i < s.size(); ++i) h += (1 << (s[i] - 'a'));
            m.insert(h);
        }
        int res = 0;
        for (string s : targetWords) {
            for (int i = 0; i < s.size(); ++i) {
                long long h = 0;
                for (int j = 0; j < s.size(); ++j) {
                    if (j == i) continue;
                    h += (1 << (s[j] - 'a'));
                }
                if (m.count(h)) {
                    res++;
                    break;
                }
            }
        }
        return res;
    }
};

// Use bitmask to save string
class Solution {
public:
    int wordCount(vector<string>& startWords, vector<string>& targetWords) {
        unordered_set<int> m;
        for (string s : startWords) {
            long h = 0;
            for (int i = 0; i < s.size(); ++i) h += (1 << (s[i] - 'a'));
            m.insert(h);
        }
        int res = 0;
        for (string s : targetWords) {
            for (int i = 0; i < s.size(); ++i) {
                long long h = 0;
                for (int j = 0; j < s.size(); ++j) {
                    if (j == i) continue;
                    h += (1 << (s[j] - 'a'));
                }
                if (m.count(h)) {
                    res++;
                    break;
                }
            }
        }
        return res;
    }
};
```
