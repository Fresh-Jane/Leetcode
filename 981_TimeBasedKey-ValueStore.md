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

/**
 * Your TimeMap object will be instantiated and called as such:
 * TimeMap* obj = new TimeMap();
 * obj->set(key,value,timestamp);
 * string param_2 = obj->get(key,timestamp);
 */
```
