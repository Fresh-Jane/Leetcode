### 706. Design HashMap (Easy)

https://leetcode.com/problems/design-hashmap/description/

```
class MyHashMap {
public:
    vector<list<pair<int, int>>> hash;
    int k = (1 << 14) + 7;
    MyHashMap() {
        hash.resize(k);
    }
    
    void put(int key, int value) {
        auto& bucket = hash[key%k];
        for (auto& p : bucket) {
            if (p.first == key) {
                p.second = value;
                return;
            }
        }
        bucket.push_back({key, value});
    }
    
    int get(int key) {
        const auto& bucket = hash[key%k];
        for (const auto& p : bucket) {
            if (p.first == key) return p.second;
        }
        return -1;
    }
    
    void remove(int key) {
        auto& bucket = hash[key%k];
        bucket.remove_if([key](const auto& p) { return p.first == key; });
    }
};

/**
 * Your MyHashMap object will be instantiated and called as such:
 * MyHashMap* obj = new MyHashMap();
 * obj->put(key,value);
 * int param_2 = obj->get(key);
 * obj->remove(key);
 */
```
