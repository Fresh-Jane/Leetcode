### 1268. Search Suggestions System (Medium)

https://leetcode.com/problems/search-suggestions-system/

```
// In one sorted string array, for any A[i], all its suggested words are following the word.
// If A[i] has the same prefix as the A[j], it has the same one with the A[i+1],,,A[j]
class Solution {
public:
    vector<vector<string>> suggestedProducts(vector<string>& products, string searchWord) {
        auto it = products.begin();
        sort(it, products.end());
        vector<vector<string>> res;
        string cur = "";
        for (char c : searchWord) {
            cur += c;
            vector<string> suggest;
            it = lower_bound(it, products.end(), cur);
            for (int i = 0; i < 3 && it + i != products.end(); ++i) {
                string& s = *(it + i);
                if (s.find(cur)) break;
                suggest.push_back(s);
            }
            res.push_back(suggest);
        }
        return res;
    }
};
```
