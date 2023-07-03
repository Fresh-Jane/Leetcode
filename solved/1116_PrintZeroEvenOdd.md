### 1116. Print Zero Even Odd (Medium)

https://leetcode.com/problems/print-zero-even-odd/description/

```
class ZeroEvenOdd {
private:
    int n;
    int i;
    bool is_zero;
    condition_variable cv;
    mutex m;

public:
    ZeroEvenOdd(int n) {
        this->n = n;
        this->i = 1;
        this->is_zero = true;
    }

    // printNumber(x) outputs "x", where x is an integer.
    void zero(function<void(int)> printNumber) {
        while(true) {
            unique_lock<mutex> lock(m);
            cv.wait(lock, [this](){ return is_zero == true || i > n; });
            if (i > n) return;
            printNumber(0);
            is_zero = false;
            cv.notify_all();
        }
    }

    void even(function<void(int)> printNumber) {
        while(true) {
            unique_lock<mutex> lock(m);
            cv.wait(lock, [this](){ return (is_zero == false && i % 2 == 0) || i > n; });
            if (i > n) return;
            printNumber(i++);
            is_zero = true;
            cv.notify_all();
        }
    }

    void odd(function<void(int)> printNumber) {
        while(true) {
            unique_lock<mutex> lock(m);
            cv.wait(lock, [this](){ return (is_zero == false && i % 2 == 1) || i > n; });
            if (i > n) return;
            printNumber(i++);
            is_zero = true;
            cv.notify_all();
        }        
    }
};
```
