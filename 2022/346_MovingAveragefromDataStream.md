### 346. Moving Average from Data Stream (Easy)

https://leetcode.com/problems/moving-average-from-data-stream/

```
class MovingAverage {
public:
    MovingAverage(int size) {
        cap = size;
        sum = 0;
    }
    
    double next(int val) {
        if (cap <= 0) return 0.0;
        q.push_back(val);
        sum += val;
        if (q.size() > cap) {
            sum -= q.front();
            q.pop_front();
        }
        return sum * 1.0 / q.size();
    }
private:
    deque<int> q;
    int cap;
    int sum;
};

/**
 * Your MovingAverage object will be instantiated and called as such:
 * MovingAverage* obj = new MovingAverage(size);
 * double param_1 = obj->next(val);
 */
```
