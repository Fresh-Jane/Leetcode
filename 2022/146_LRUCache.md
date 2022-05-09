### 146. LRU Cache (Medium)

https://leetcode.com/problems/lru-cache/

```
class LRUCache {
public:
    LRUCache(int capacity) {
        cap = capacity;
    }
    
    int get(int key) {
        auto it = table.find(key);
        if (it == table.end()) return -1;
        auto cit = it->second;
        int val = cit->second;
        cache.splice(cache.begin(), cache, cit);
        table[key] = cache.begin();
        return val;
    }
    
    void put(int key, int value) {
        if (get(key) != -1) {
            table[key]->second = value;
        } else {
            if (cache.size() == cap) {
                int k = cache.back().first;
                table.erase(k);
                cache.pop_back();
            }
            cache.push_front({key, value});
            table[key] = cache.begin();
        }
    }
private:
    using Cache = list<pair<int, int>>;
    Cache cache;
    unordered_map<int, Cache::iterator> table;
    int cap;
};

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache* obj = new LRUCache(capacity);
 * int param_1 = obj->get(key);
 * obj->put(key,value);
 */
```
