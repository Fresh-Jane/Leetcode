### 1114. Print in Order (Easy)

https://leetcode.com/problems/print-in-order/description/

```
// Use mutex
class Foo {
private:
    mutex m1, m2, m3;
public:
    Foo() {
        m2.lock();
        m3.lock();
    }

    void first(function<void()> printFirst) {
        m1.lock();
        // printFirst() outputs "first". Do not change or remove this line.
        printFirst();
        m2.unlock();
    }

    void second(function<void()> printSecond) {
        m2.lock();
        // printSecond() outputs "second". Do not change or remove this line.
        printSecond();
        m3.unlock();
    }

    void third(function<void()> printThird) {
        m3.lock();
        // printThird() outputs "third". Do not change or remove this line.
        printThird();
        m1.unlock();
    }
};

// Use condition_variable
class Foo {
private:
    condition_variable cv;
    mutex m;
    int index = 1;
public:
    Foo() {
    }

    void first(function<void()> printFirst) {
        unique_lock<mutex> lock(m);
        cv.wait(lock, [this](){ return index == 1; });
        cv.notify_all();
        index = 2;
        // printFirst() outputs "first". Do not change or remove this line.
        printFirst();
    }

    void second(function<void()> printSecond) {
        unique_lock<mutex> lock(m);
        cv.wait(lock, [this](){ return index == 2; });
        cv.notify_all();
        index = 3;
        // printSecond() outputs "second". Do not change or remove this line.
        printSecond();
    }

    void third(function<void()> printThird) {
        unique_lock<mutex> lock(m);
        cv.wait(lock, [this](){ return index == 3; });
        cv.notify_all();
        index = 1;        
        // printThird() outputs "third". Do not change or remove this line.
        printThird();
    }
};

// Use atomic
class Foo {
private:
    atomic<int> turn;
public:
    Foo() {
        turn = 1;
    }

    void first(function<void()> printFirst) {
        while(turn != 1) {
            this_thread::yield();
        }
        // printFirst() outputs "first". Do not change or remove this line.
        printFirst();
        ++turn;
    }

    void second(function<void()> printSecond) {
        while(turn != 2) {
            this_thread::yield();
        }
        // printSecond() outputs "second". Do not change or remove this line.
        printSecond();
        ++turn;
    }

    void third(function<void()> printThird) {
        while(turn != 3) {
            this_thread::yield();
        }
        // printThird() outputs "third". Do not change or remove this line.
        printThird();
    }
};
```
