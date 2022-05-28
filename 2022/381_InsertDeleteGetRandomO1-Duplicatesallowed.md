### 381. Insert Delete GetRandom O(1) - Duplicates allowed (Hard)

https://leetcode.com/problems/insert-delete-getrandom-o1-duplicates-allowed/

```
class RandomizedCollection {
public:
    RandomizedCollection() {}
    
    bool insert(int val) {
        bool res = !m.count(val);
        num.push_back(val);
        m[val].insert(num.size() - 1);
        return res;
    }
    
    bool remove(int val) {
        if (!m.count(val)) return false;
        if (val == num.back()) {
            m[val].erase(num.size()-1);
            num.pop_back();
        } else {
            int index = *m[val].begin();
            int nn = num.back();
            num[index] = nn;
            m[nn].erase(num.size()-1);
            m[nn].insert(index);
            m[val].erase(index);
            num.pop_back();
        }
        if (m[val].empty()) m.erase(val);
        return true;
    }
    
    int getRandom() {
        return num[rand()%num.size()];
    }
private:
    unordered_map<int, unordered_set<int>> m;
    vector<int> num;
};

/**
 * Your RandomizedCollection object will be instantiated and called as such:
 * RandomizedCollection* obj = new RandomizedCollection();
 * bool param_1 = obj->insert(val);
 * bool param_2 = obj->remove(val);
 * int param_3 = obj->getRandom();
 */
```
