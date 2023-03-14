### 1146. Snapshot Array (Medium)

https://leetcode.com/problems/snapshot-array/

```
class SnapshotArray {
public:
    SnapshotArray(int length) {
        arr.resize(length);
        for (int i = 0; i < length; ++i) arr[i].push_back({snap_num, 0});
    }
    
    void set(int index, int val) {
        auto& h = arr[index];
        if (h.back().first < snap_num) h.push_back({snap_num, val});
        else h.back().second = val;
    }
    
    int snap() {
        return snap_num++;
    }
    
    int get(int index, int snap_id) {
        assert(snap_id < snap_num);
        const auto& h = arr[index];
        auto it = upper_bound(h.begin(), h.end(), snap_id,
            [](int id, const pair<int, int>& p) {
                return id < p.first;
            });
        return prev(it)->second;
    }
private:
    vector<vector<pair<int, int>>> arr;
    int snap_num = 0;
};

/**
 * Your SnapshotArray object will be instantiated and called as such:
 * SnapshotArray* obj = new SnapshotArray(length);
 * obj->set(index,val);
 * int param_2 = obj->snap();
 * int param_3 = obj->get(index,snap_id);
 */
```
