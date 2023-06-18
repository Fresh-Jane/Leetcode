### 953. Verifying an Alien Dictionary (Easy)

https://leetcode.com/problems/verifying-an-alien-dictionary/description/

```
class Solution {
public:
    bool isAlienSorted(vector<string>& words, string order) {
        vector<int> m(26);
        for (int i = 0; i < 26; ++i) m[order[i]-'a'] = i;
        for (int i = 0; i < words.size() - 1; ++i) 
            if (!InOrder(words[i], words[i+1], m)) return false;
        return true;
    }
    bool InOrder(const string& word1, const string& word2, const vector<int>& m) {
        for (int i = 0; i < word1.size(); ++i) {
            if (i == (int)word2.size()) return false;
            if (m[word1[i]-'a'] < m[word2[i]-'a']) return true;
            if (m[word1[i]-'a'] > m[word2[i]-'a']) return false;
        }
        return true;
    }
};
```
