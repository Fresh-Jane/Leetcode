### 243. Shortest Word Distance (Easy)

https://leetcode.com/problems/shortest-word-distance/

```
class Solution {
public:
    int shortestDistance(vector<string>& wordsDict, string word1, string word2) {
        int res = wordsDict.size();
        int i1 = -1, i2 = -1;
        for (int i = 0; i < wordsDict.size(); ++i) {
            if (wordsDict[i] == word1) i1 = i;
            else if (wordsDict[i] == word2) i2 = i;
            if (i1 != -1 && i2 != -1) res = min(res, abs(i1 - i2));
        }
        return res;
    }
};
```
