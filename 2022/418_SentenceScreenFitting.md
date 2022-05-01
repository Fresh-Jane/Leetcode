### 418. Sentence Screen Fitting (Medium)

https://leetcode.com/problems/sentence-screen-fitting/

```
class Solution {
public:
    int wordsTyping(vector<string>& sentence, int rows, int cols) {
        const int n = sentence.size(); 
        vector<int> dp(n, 0); // The number of words fitted into one row started with sentence[i]
        int words = 0;
        while(rows--) {
            const int i = words % n;
            if (!dp[i]) {
                int j = i, len = 0;
                while(len + sentence[j].size() <= cols) {
                    len += sentence[j].size() + 1;
                    j = (j+1) % n;
                    ++dp[i];
                }
            } 
            words+=dp[i];
        }
        return words / n;
    }
};
```
