### 1239. Maximum Length of a Concatenated String with Unique Characters (Medium)

https://leetcode.com/problems/maximum-length-of-a-concatenated-string-with-unique-characters/description/

```
class Solution {
public:
    int maxLength(vector<string>& arr) {
        unordered_set<int> bit_word_set;
        for (const string& word : arr) wordToBit(bit_word_set, word);
        vector<int> bit_word_vec(bit_word_set.begin(), bit_word_set.end());
        return dfs(bit_word_vec, 0, 0);
    }
    void wordToBit(unordered_set<int>& bit_word_set, const string& word) {
        int bit_word = 0;
        for (const char& c : word) {
            const int bit_c = 1 << (c - 'a');
            if (bit_word & bit_c) return;
            bit_word += bit_c;
        }
        bit_word += (word.size() << 26);
        bit_word_set.insert(bit_word);
    }
    int dfs(const vector<int>& bit_word_vec, int pos, int res) {
        int oldChars = res & ((1 << 26) - 1);
        int oldLen = res >> 26;
        int best = oldLen;
        for (int i = pos; i < bit_word_vec.size(); ++i) {
            int newChars = bit_word_vec[i] & ((1 << 26) - 1);
            int newLen = bit_word_vec[i] >> 26;
            if (oldChars & newChars) continue;
            int newRes = newChars + oldChars + (newLen + oldLen << 26);
            best = max(best, dfs(bit_word_vec, i + 1, newRes));
        }
        return best;
    }
};
```
