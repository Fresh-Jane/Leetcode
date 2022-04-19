### 809. Expressive Words (Medium)

Sometimes people repeat letters to represent extra feeling, such as "hello" -> "heeellooo", "hi" -> "hiiii".  In these strings like "heeellooo", we have groups of adjacent letters that are all the same:  "h", "eee", "ll", "ooo".

For some given string S, a query word is stretchy if it can be made to be equal to S by any number of applications of the following extension operation: choose a group consisting of characters c, and add some number of characters c to the group so that the size of the group is 3 or more.

For example, starting with "hello", we could do an extension on the group "o" to get "hellooo", but we cannot get "helloo" since the group "oo" has size less than 3.  Also, we could do another extension like "ll" -> "lllll" to get "helllllooo".  If S = "helllllooo", then the query word "hello" would be stretchy because of these two extension operations: query = "hello" -> "hellooo" -> "helllllooo" = S.

Given a list of query words, return the number of words that are stretchy. 

```
Example:
Input: 
S = "heeellooo"
words = ["hello", "hi", "helo"]
Output: 1
Explanation: 
We can extend "e" and "o" in the word "hello" to get "heeellooo".
We can't extend "helo" to get "heeellooo" because the group "ll" is not size 3 or more.
```

Constraints:

- 0 <= len(S) <= 100.
- 0 <= len(words) <= 100.
- 0 <= len(words[i]) <= 100.
- S and all words in words consist only of lowercase letters

```
// Two pointer
class Solution 1 {
public:
    int expressiveWords(string S, vector<string>& words) {
        int res = 0;
        for (auto &W : words) if (check(S, W)) res++;
        return res;
    }

    bool check(string S, string W) {
        int n = S.size(), m = W.size(), j = 0;
        for (int i = 0; i < n; i++)
            if (j < m && S[i] == W[j]) j++;
            else if (i > 1 && S[i - 2] == S[i - 1] && S[i - 1] == S[i]);
            else if (0 < i && i < n - 1 && S[i - 1] == S[i] && S[i] == S[i + 1]);
            else return false;
        return j == m;
    }
};

class Solution 2 {
public:
    bool isStrechy(string S, string w) {
        int i = 0, j = 0;
        const int slen = S.size(), wlen = w.size();
        if (slen < wlen) return false;
        while (i < slen && j < wlen) {
            if (S[i] != w[j]) return false;
            int si = i, wi = j;
            while (i < slen && S[i] == S[si]) i++;
            while (j < wlen && w[j] == w[wi]) j++;
            const int sl = i - si, wl = j - wi;
            if (wl > sl || (sl > wl && sl < 3)) return false;
        }
        return i >= slen;
    }
    int expressiveWords(string S, vector<string>& words) {
        int res = 0;
        for (const string w : words) 
            if (isStrechy(S, w)) res++;
        return res;
    }
};
```
