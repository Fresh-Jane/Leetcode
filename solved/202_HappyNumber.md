### 202. Happy Number (Easy)

https://leetcode.com/problems/happy-number/description/

```
// Two pointer, like linkedList find cycle
class Solution {
public:
    bool isHappy(int n) {
        int slow = n, fast = n;
        while(true) {
            slow = next(slow);
            fast = next(next(fast));
            if (slow == fast) break;
        }
        return slow == 1;
    }
    int next(int cur) {
        int sum = 0;
        while(cur) {
            sum += (cur % 10) * (cur % 10);
            cur /= 10;
        }
        return sum;
    }
};

// hashtable
class Solution {
public:
    bool isHappy(int n) {
        unordered_set<int> s;
        s.insert(n);
        while(true) {
            int sum = 0;
            while(n) {
                sum += (n % 10) * (n % 10);
                n /= 10;
            }
            if (sum == 1) return true;
            if (s.count(sum)) break;
            s.insert(sum);
            n = sum;
        }
        return false;
    }
};
```
