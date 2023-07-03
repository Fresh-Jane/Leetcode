### 1226. The Dining Philosophers (Medium)

https://leetcode.com/problems/the-dining-philosophers/description/

```
class DiningPhilosophers {
private:
    condition_variable cv;
    mutex m;
    vector<bool> fork_can_pick;
public:
    DiningPhilosophers() {
        fork_can_pick.resize(5, true);
    }

    void wantsToEat(int philosopher,
                    function<void()> pickLeftFork,
                    function<void()> pickRightFork,
                    function<void()> eat,
                    function<void()> putLeftFork,
                    function<void()> putRightFork) {
        const int fork_index = (philosopher + 1) % 5;
        {
            unique_lock<mutex> lp(m);
            cv.wait(lp, [&](){ return fork_can_pick[philosopher] && fork_can_pick[fork_index]; });
            pickLeftFork();
            fork_can_pick[philosopher] = false;
            pickRightFork();
            fork_can_pick[fork_index] = false;
        }
        eat();
        {
            unique_lock<mutex> lp(m);
            putLeftFork();
            fork_can_pick[philosopher] = true;
            putRightFork();
            fork_can_pick[fork_index] = true;
        }
        cv.notify_all();
    }
};
```
