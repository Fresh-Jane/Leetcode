### 792. Number of Matching Subsequences (Medium)

Given string S and a dictionary of words words, find the number of words[i] that is a subsequence of S.

```
Example :
Input: 
S = "abcde"
words = ["a", "bb", "acd", "ace"]
Output: 3
Explanation: There are three words in words that are a subsequence of S: "a", "acd", "ace".
```

Note:

- All words in words and S will only consists of lowercase letters.
- The length of S will be in the range of [1, 50000].
- The length of words will be in the range of [1, 5000].
- The length of words[i] will be in the range of [1, 50].

```
// Binary search
class Solution 1 {
public:
    int numMatchingSubseq(string S, vector<string>& words) {
        int num = 0;
        vector<vector<int>> order_map(26);
        for (int i = 0; i < S.size(); ++i) order_map[S[i]-'a'].push_back(i);
        for (const string& w : words) {
            int max_s_index = -1;
            bool is_sub = true;
            for (const char c : w) {
                const vector<int>& o = order_map[c-'a'];
                auto cur = upper_bound(o.begin(), o.end(), max_s_index);
                if (cur == o.end()) is_sub = false;
                else max_s_index = *cur;
            }
            if (is_sub) num++;
        }
        return num;
    }
};

// TLE
class Solution 2 {
public:
    bool isSubseq(string S, string w) {
        int iter_s = 0, iter_w = 0;
        int len_s = S.size(), len_w = w.size();
        while(iter_w < len_w && iter_s < len_s) {
            if(w[iter_w] == S[iter_s]) iter_w++;
            iter_s++;
        }
        return iter_w == len_w;
    }
    int numMatchingSubseq(string S, vector<string>& words) {
        int num = 0;
        for (const string& w : words) 
            if (isSubseq(S, w)) num++;
        return num;
    }
};
```
