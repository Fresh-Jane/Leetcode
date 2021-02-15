### 471. Encode String with Shortest Length (Hard)

Given a non-empty string, encode the string such that its encoded length is the shortest.

The encoding rule is: k[encoded_string], where the encoded_string inside the square brackets is being repeated exactly k times.

Note:

- k will be a positive integer.
- If an encoding process does not make the string shorter, then do not encode it. If there are several solutions, return any of them.
 
Example 1:

```
Input: s = "aaa"
Output: "aaa"
Explanation: There is no way to encode it such that it is shorter than the input string, so we do not encode it.
```
Example 2:

```
Input: s = "aaaaa"
Output: "5[a]"
Explanation: "5[a]" is shorter than "aaaaa" by 1 character.
```
Example 3:

```
Input: s = "aaaaaaaaaa"
Output: "10[a]"
Explanation: "a9[a]" or "9[a]a" are also valid solutions, both of them have the same length = 5, which is the same as "10[a]".
```
Example 4:

```
Input: s = "aabcaabcd"
Output: "2[aabc]d"
Explanation: "aabc" occurs twice, so one answer can be "2[aabc]d".
```
Example 5:

```
Input: s = "abbbabbbcabbbabbbc"
Output: "2[2[abbb]c]"
Explanation: "abbbabbbc" occurs twice, but "abbbabbbc" can also be encoded to "2[abbb]c", so one answer can be "2[2[abbb]c]".
```

Constraints:

- 1 <= s.length <= 150
- s consists of only lowercase English letters.

```
// DFS
// Time: O(m^3)
// Space: O(m)
class Solution 1 {
public:
    int numRepetition(const string& s, const string& s1) {
        const int len = s.size();
        int cnt = 0, index = 0;
        while (index < len) {
            if (s.substr(index, s1.size()) != s1) break;
            cnt++;
            index += s1.size(); 
        }
        return cnt;
    }
    
    string dfs(string s, unordered_map<string, string>& m) {
        if (s.size() < 5) return s;
        if (m.count(s)) return m[s];
        string res = s, cur_res = s;
        for (int i = 0; i < s.size(); ++i) {
            const string s1 = s.substr(0, i+1);
            const int cnt = numRepetition(s, s1);
            for (int k = 1; k <= cnt; ++k) {
                if (k == 1) cur_res = s1 + dfs(s.substr(i+1), m);
                else cur_res = to_string(k) + "[" + dfs(s1, m) + "]" + dfs(s.substr(k*s1.size()), m);
                if (cur_res.size() < res.size()) res = cur_res;
            }
        }
        m[s] = res;
        return res;
    }
    
    string encode(string s) {
        unordered_map<string, string> m;
        return dfs(s, m);
    }
};

// DP
// Time: O(m^3)
// Space: O(m^2)
class Solution 2 {
public:
    string collapse(string s, int i, int step) {
        string temp = s.substr(i, step);
        const auto pos = (temp+temp).find(temp, 1);
        if (pos >= temp.size()) {
            return temp;
        }
        return to_string(temp.size()/pos) + "[" + dp[i][i+pos-1] + "]";
    }
    
    string encode(string s) {
        const int m = s.size();
        if (m < 5) return s;
        dp = vector<vector<string>>(m, vector<string>(m, ""));
        for (int step = 1; step <= m; ++step) {
            for (int i = 0; i + step -1 < m; ++i) {
                int j = i + step - 1;
                dp[i][j] = s.substr(i, step);
                for (int k = i; k < j; ++k) {
                    string left = dp[i][k], right = dp[k+1][j];
                    if (left.size() + right.size() < dp[i][j].size()) {
                        dp[i][j] = left + right;
                    }
                }
                string self = collapse(s, i, step);
                if (self.size() < dp[i][j].size()) {
                    dp[i][j] = self;
                }
            }
        }
        return dp[0][m-1];
    }
private:
    vector<vector<string>> dp;
};

```
