### 245. Shortest Word Distance III (Medium)

https://leetcode.com/problems/shortest-word-distance-iii/

```
class Solution {
public:
    int shortestWordDistance(vector<string>& wordsDict, string word1, string word2) {
        const int n = wordsDict.size();
        int min_dis = n - 1;
        int p1 = -1, p2 = -1;
        bool e = word1 == word2;
        for (int i = 0; i < wordsDict.size(); ++i) {
            if (wordsDict[i] == word1) {
                p1 = i;
                if (p2 != -1) min_dis = min(min_dis, p1 - p2);
                if (e) p2 = i;
            } else if (!e && wordsDict[i] == word2) {
                p2 = i;
                if (p1 != -1) min_dis = min(min_dis, p2 - p1);
            }
        }
        return min_dis;
    }
};
```
