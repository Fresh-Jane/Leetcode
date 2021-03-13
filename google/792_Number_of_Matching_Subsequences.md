### 792. Number of Matching Subsequences (Medium)

Given a string s and an array of strings words, return the number of words[i] that is a subsequence of s.

A subsequence of a string is a new string generated from the original string with some characters (can be none) deleted without changing the relative order of the remaining characters.

For example, "ace" is a subsequence of "abcde".
 
Example 1:

```
Input: s = "abcde", words = ["a","bb","acd","ace"]
Output: 3
Explanation: There are three strings in words that are a subsequence of s: "a", "acd", "ace".
```
Example 2:

```
Input: s = "dsahjpjauf", words = ["ahjpjau","ja","ahbwzgqnuk","tnmlanowax"]
Output: 2
```

Constraints:

- 1 <= s.length <= 5 * 10^4
- 1 <= words.length <= 5000
- 1 <= words[i].length <= 50
- s and words[i] consist of only lowercase English letters.

```
class Solution {
public:
    int numMatchingSubseq (string S, vector<string>& words) {
		vector<const char*> waiting[128];
        for (string &w : words) 
            waiting[w[0]].push_back(w.c_str());
        for (const auto& c : S) {
            auto advance = waiting[c];
            waiting[c].clear();
            for (auto it : advance) {
                waiting[*++it].push_back(it);
            }
        }
        return waiting[0].size();
	}
};
```
