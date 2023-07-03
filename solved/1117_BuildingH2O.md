### 1117. Building H2O (Medium)

https://leetcode.com/problems/building-h2o/description/

```
class H2O {
private:
    condition_variable cv;
    mutex m;
    int hn;
public:
    H2O() {
        hn = 0;
    }

    void hydrogen(function<void()> releaseHydrogen) {
        unique_lock<mutex> lock(m);
        cv.wait(lock, [this](){ return hn < 2; });
        // releaseHydrogen() outputs "H". Do not change or remove this line.
        releaseHydrogen();
        ++hn;
        cv.notify_all();
    }

    void oxygen(function<void()> releaseOxygen) {
        unique_lock<mutex> lock(m);
        cv.wait(lock, [this](){ return hn == 2; });
        // releaseOxygen() outputs "O". Do not change or remove this line.
        releaseOxygen();
        hn = 0;
        cv.notify_all();
    }
};
```
