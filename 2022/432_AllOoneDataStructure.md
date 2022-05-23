### 432. All O`one Data Structure (Hard)

https://leetcode.com/problems/all-oone-data-structure/

```
class AllOne {
public:
    AllOne() {}
    
    void inc(string key) {
        if (cnt_m.count(key)) {
            m[cnt_m[key]].erase(key);
            if (m[cnt_m[key]].empty()) m.erase(cnt_m[key]);
        }
        cnt_m[key]++;
        m[cnt_m[key]].insert(key);
    }
    
    void dec(string key) {
        if (cnt_m.count(key)) {
            m[cnt_m[key]].erase(key);
            if (m[cnt_m[key]].empty()) m.erase(cnt_m[key]);
        }
        if (--cnt_m[key] == 0) cnt_m.erase(key);
        else m[cnt_m[key]].insert(key);
    }
    
    string getMaxKey() {
        return m.empty() ? "" : *(m.rbegin()->second.begin());
    }
    
    string getMinKey() {
        return m.empty() ? "" : *(m.begin()->second.begin());
    }
private:
    unordered_map<string, int> cnt_m;
    map<int, unordered_set<string>> m;
};

/**
 * Your AllOne object will be instantiated and called as such:
 * AllOne* obj = new AllOne();
 * obj->inc(key);
 * obj->dec(key);
 * string param_3 = obj->getMaxKey();
 * string param_4 = obj->getMinKey();
 */
```
