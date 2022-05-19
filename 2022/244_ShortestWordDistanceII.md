### 244. Shortest Word Distance II (Medium)

https://leetcode.com/problems/shortest-word-distance-ii/

```
class WordDistance {
public:
    WordDistance(vector<string>& wordsDict) {
        for (int i = 0; i < wordsDict.size(); ++i) 
            m[wordsDict[i]].push_back(i);
    }
    // Use binary search
    int shortest(string word1, string word2) {
        int min_dis = INT_MAX;
        const vector<int>& pos2 = m[word2];
        for (int index1 : m[word1]) {
            auto in2 = lower_bound(pos2.begin(), pos2.end(), index1);
            if (in2 != pos2.end()) min_dis = min(min_dis, abs(*in2 - index1));
            if (in2 != pos2.begin()) min_dis = min(min_dis, abs(*(in2-1) - index1));
        }
        return min_dis;
    }
private:
    unordered_map<string, vector<int>> m;
};

/**
 * Your WordDistance object will be instantiated and called as such:
 * WordDistance* obj = new WordDistance(wordsDict);
 * int param_1 = obj->shortest(word1,word2);
 */
```
