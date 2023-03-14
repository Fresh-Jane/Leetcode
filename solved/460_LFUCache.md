### 460. LFU Cache (Hard)

https://leetcode.com/problems/lfu-cache/

```
class LFUCache {
public:
    LFUCache(int capacity) {
        cap = capacity;
        cnt = min_fre = 0;
    }
    
    int get(int key) {
        if (!km.count(key)) return -1;
        else {
            fm[km[key].fre].erase(km[key].pos);
            km[key].fre++;
            fm[km[key].fre].push_front(key);
            km[key].pos = fm[km[key].fre].begin();
            if(fm[min_fre].empty()) {
                fm.erase(min_fre);
                min_fre++;
            }
            return km[key].val;
        } 
    }
    
    void put(int key, int value) {
        if (cap == 0) return;
        if (get(key) != -1) {
            km[key].val = value;
        } else {
            if (cnt == cap) {
                km.erase(fm[min_fre].back());
                fm[min_fre].pop_back();
                cnt--;
            }
            fm[1].push_front(key);
            km[key] = {value, 1, fm[1].begin()};
            min_fre = 1;
            cnt++;
        }
    }
private:
    struct keyInfo {
        int val, fre;
        list<int>::iterator pos;
    };
    unordered_map<int, keyInfo> km;
    unordered_map<int, list<int>> fm;
    int cap, cnt, min_fre;
};

/**
 * Your LFUCache object will be instantiated and called as such:
 * LFUCache* obj = new LFUCache(capacity);
 * int param_1 = obj->get(key);
 * obj->put(key,value);
 */
```
