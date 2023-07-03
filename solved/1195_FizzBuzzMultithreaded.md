### 1195. Fizz Buzz Multithreaded (Medium)

https://leetcode.com/problems/fizz-buzz-multithreaded/description/

```
// Use condition_variable

class FizzBuzz {
private:
    int n;
    int i;
    condition_variable cv;
    mutex m;

public:
    FizzBuzz(int n) {
        this->n = n;
        this->i = 1;
    }

    // printFizz() outputs "fizz".
    void fizz(function<void()> printFizz) {
        while (true) {
            unique_lock<mutex> lock(m);
            cv.wait(lock, [this](){ return (i % 3 == 0 && i % 5 != 0) || i > n; });
            if (i > n) return;
            printFizz();
            ++i;
            cv.notify_all(); 
        }
    }

    // printBuzz() outputs "buzz".
    void buzz(function<void()> printBuzz) {
        while (true) {
            unique_lock<mutex> lock(m);
            cv.wait(lock, [this](){ return (i % 3 != 0 && i % 5 == 0) || i > n; });
            if (i > n) return;
            printBuzz();
            ++i;
            cv.notify_all();
        }         
    }

    // printFizzBuzz() outputs "fizzbuzz".
	void fizzbuzz(function<void()> printFizzBuzz) {
        while (true) {
            unique_lock<mutex> lock(m);
            cv.wait(lock, [this](){ return i % 15 == 0 || i > n; });
            if (i > n) return;
            printFizzBuzz();
            ++i;
            cv.notify_all();
        }        
    }

    // printNumber(x) outputs "x", where x is an integer.
    void number(function<void(int)> printNumber) {
        while (true) {
            unique_lock<mutex> lock(m);
            cv.wait(lock, [this](){ return (i % 3 != 0 && i % 5 != 0) || i > n; });
            if (i > n) return;
            printNumber(i);
            ++i;
            cv.notify_all();
        }
    }
};
```
