### 460. LFU Cache (Hard)

https://leetcode.com/problems/lfu-cache/ 

```
class LFUCache {
public:
    LFUCache(int capacity) {
        this->capacity = capacity;
        min_fre = count = 0;
    }
    
    int get(int key) {
        if (!node_m.count(key)) return -1;
        fre_m[node_m[key].fre].erase(node_m[key].pos);
        node_m[key].fre++;
        fre_m[node_m[key].fre].push_front(key);
        node_m[key].pos = fre_m[node_m[key].fre].begin();
        if (fre_m[min_fre].empty()) {
            fre_m.erase(min_fre);
            min_fre++;
        }
        return node_m[key].val;
    }
    
    void put(int key, int value) {
        if (capacity == 0) return;
        if (get(key) != -1) {
            node_m[key].val = value;
        } else {
            if (count == capacity) {
                node_m.erase(fre_m[min_fre].back());
                fre_m[min_fre].pop_back();
                --count;
            }
            fre_m[1].push_front(key);
            node_m[key] = {value, 1, fre_m[1].begin()};
            ++count;
            min_fre = 1;
        }
    }
private:
    struct Node {
        int val, fre;
        list<int>::iterator pos;
    };
    unordered_map<int, Node> node_m;   // (key, Node)
    unordered_map<int, list<int>> fre_m;  // (fre, list of key)
    int capacity, min_fre, count;
};

/**
 * Your LFUCache object will be instantiated and called as such:
 * LFUCache* obj = new LFUCache(capacity);
 * int param_1 = obj->get(key);
 * obj->put(key,value);
 */
```
