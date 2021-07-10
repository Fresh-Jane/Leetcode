### 692. Top K Frequent Words (Medium)

https://leetcode.com/problems/top-k-frequent-words/

```
class Solution {
public:
    vector<string> topKFrequent(vector<string>& words, int k) {
        unordered_map<string, int> num_map;
        for (const string& w : words) ++num_map[w];
        using It = unordered_map<string, int>::const_iterator;
        struct cmp {
            bool operator() (const It& i1, const It& i2) const {
                if (i1->second == i2->second) return i1->first < i2->first;
                return i1->second > i2->second;
            }
        };
        priority_queue<It, vector<It>, cmp> q;
        for (It i = num_map.begin(); i != num_map.end(); ++i) {
            q.push(i);
            if (!q.empty() && q.size() > k) q.pop();
        }
        vector<string> res;
        res.reserve(k);
        while (k) {
            res.push_back(q.top()->first);
            q.pop();
            k--;
        }
        reverse(res.begin(), res.end());
        return res;
    }
};
```
