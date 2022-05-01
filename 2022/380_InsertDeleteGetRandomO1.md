### 380_InsertDeleteGetRandomO(1) (Medium)

https://leetcode.com/problems/insert-delete-getrandom-o1/

```
class RandomizedSet {
public:
    RandomizedSet() {}
    
    bool insert(int val) {
        if (m.count(val)) return false;
        nums.push_back(val);
        m[val] = nums.size() - 1;
        return true;
    }
    
    bool remove(int val) {
        auto it = m.find(val);
        if (it == m.end()) return false;
        int i = it->second;
        m[nums.back()] = i;
        swap(nums[i], nums.back());
        nums.pop_back();
        m.erase(it);
        return true;
    }
    
    int getRandom() {
        return nums[rand() % nums.size()];
    }
private:
    vector<int> nums;
    unordered_map<int, int> m;
};

/**
 * Your RandomizedSet object will be instantiated and called as such:
 * RandomizedSet* obj = new RandomizedSet();
 * bool param_1 = obj->insert(val);
 * bool param_2 = obj->remove(val);
 * int param_3 = obj->getRandom();
 */
```
