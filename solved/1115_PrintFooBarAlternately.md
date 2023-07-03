### 1115. Print FooBar Alternately (Medium)

https://leetcode.com/problems/print-foobar-alternately/description/

```
// https://leetcode.com/problems/print-foobar-alternately/solutions/2392439/c-c-3-ways-to-solve-atomic-mutex-semaphore/

// use condition_variable
class FooBar {
private:
    int n;
    condition_variable cv;
    mutex m;
    bool t_value = false;
public:
    FooBar(int n) {
        this->n = n;
    }

    void foo(function<void()> printFoo) {
        for (int i = 0; i < n; i++) {
            unique_lock<mutex> lock(m);
            cv.wait(lock,[this](){ return t_value == false; });
            cv.notify_one();
            t_value = true;
        	// printFoo() outputs "foo". Do not change or remove this line.
        	printFoo();
        }
    }

    void bar(function<void()> printBar) {
        for (int i = 0; i < n; i++) {
            unique_lock<mutex> lock(m);
            cv.wait(lock,[this](){ return t_value == true; });
            cv.notify_one();
            t_value = false;
        	// printBar() outputs "bar". Do not change or remove this line.
        	printBar();
        }
    }
};


// Use atomic
class FooBar {
private:
    int n;
    atomic<bool> alt;

public:
    FooBar(int n) {
        this->n = n;
        alt = false;
    }

    void foo(function<void()> printFoo) {
        
        for (int i = 0; i < n; i++) {
            while(alt) {
                this_thread::yield();
            }
            
        	// printFoo() outputs "foo". Do not change or remove this line.
        	printFoo();

            alt = !alt;
        }
    }

    void bar(function<void()> printBar) {
        
        for (int i = 0; i < n; i++) {
            while(!alt) {
                this_thread::yield();
            }
            
        	// printBar() outputs "bar". Do not change or remove this line.
        	printBar();
            alt = !alt;
        }
    }
};

// Use mutex
class FooBar {
private:
    int n;
    mutex foom;
    mutex barm;

public:
    FooBar(int n) {
        this->n = n;
        barm.lock();
    }

    void foo(function<void()> printFoo) {
        
        for (int i = 0; i < n; i++) {
            foom.lock();
        	// printFoo() outputs "foo". Do not change or remove this line.
        	printFoo();
            barm.unlock();
        }
    }

    void bar(function<void()> printBar) {
        
        for (int i = 0; i < n; i++) {
            barm.lock();
        	// printBar() outputs "bar". Do not change or remove this line.
        	printBar();
            foom.unlock();
        }
    }
};
```
