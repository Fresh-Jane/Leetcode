### 981. Time Based Key-Value Store (Medium)

https://leetcode.com/problems/time-based-key-value-store/

```
// map is implemented by red black tree which is a BST and can use upper_bound operation.
// Red black tree offers the logrithmic complexity for insertion, search and deletion. 
class TimeMap {
public:
    TimeMap() {}
    
    void set(string key, string value, int timestamp) {
        m[key][timestamp] = value;
    }
    
    string get(string key, int timestamp) {
        auto it = m.find(key);
        if (it == m.end()) return "";
        const auto& t = it->second;
        auto tit = t.upper_bound(timestamp);
        if (tit == t.begin()) return "";
        return prev(tit)->second;
    }
private:
    unordered_map<string, map<int, string>> m;
};

// Use vector to implement
class TimeMap {
public:
    TimeMap() {}
    
    void set(string key, string value, int timestamp) {
        m[key].push_back({timestamp, value});
    }
    
    string get(string key, int timestamp) {
        if (!m.count(key)) return "";
        const vector<pair<int, string>>& vset = m.at(key);
        int l = 0, r = vset.size() - 1;
        while(l <= r) {
            int m = l + (r - l) / 2;
            if (vset[m].first < timestamp) l = m + 1;
            else r = m - 1;
        }
        if (l < vset.size() && vset[l].first == timestamp) return vset[l].second;
        return l == 0 ? "" : vset[l-1].second; 
    }
private:
    unordered_map<string, vector<pair<int, string>>> m;
};

/**
 * Your TimeMap object will be instantiated and called as such:
 * TimeMap* obj = new TimeMap();
 * obj->set(key,value,timestamp);
 * string param_2 = obj->get(key,timestamp);
 */
```
