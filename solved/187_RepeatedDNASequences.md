### 187. Repeated DNA Sequences (Medium)

https://leetcode.com/problems/repeated-dna-sequences/

```
// bitmap, use 3 bits to represent one char, A-001, C-011, G-111, T-110. So the sequence can be represented as 30 bits.
class Solution {
public:
    vector<string> findRepeatedDnaSequences(string s) {
        unordered_map<unsigned, int> m;
        unsigned k = 0;
        vector<string> res;
        for (int i = 0; i < (int)s.size(); ++i) {
            k = ((k << 3) & ((1 << 30) - 1)) | (s[i] & 0b111);
            if (m[k]++ == 1) res.push_back(s.substr(i-9, 10));
        }
        return res;
    }
}; 
```
