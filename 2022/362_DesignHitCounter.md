### 362. Design Hit Counter (Medium)

https://leetcode.com/problems/design-hit-counter/

```
class HitCounter {
public:
    HitCounter() {
        times.resize(300, 0);
        hits.resize(300, 0);
    }
    
    void hit(int timestamp) {
        int i = timestamp % 300;
        if (times[i] != timestamp) {
            times[i] = timestamp;
            hits[i] = 1;
        } else hits[i]++;
    }
    
    int getHits(int timestamp) {
        int res = 0;
        for (int i = 0; i < 300; ++i) 
            if (timestamp - times[i] < 300) res += hits[i];
        return res;
    }
private:
    vector<int> times, hits;
};

/**
 * Your HitCounter object will be instantiated and called as such:
 * HitCounter* obj = new HitCounter();
 * obj->hit(timestamp);
 * int param_2 = obj->getHits(timestamp);
 */
```
