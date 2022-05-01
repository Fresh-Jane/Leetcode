### 359. Logger Rate Limiter (Easy)

https://leetcode.com/problems/logger-rate-limiter/

```
class Logger {
public:
    bool shouldPrintMessage(int timestamp, string message) {
        if (!m.count(message) || timestamp - m[message] >= 10) {
            m[message] = timestamp;
            return true;
        } 
        return false;
    }
private:
    unordered_map<string, int> m;
};

/**
 * Your Logger object will be instantiated and called as such:
 * Logger* obj = new Logger();
 * bool param_1 = obj->shouldPrintMessage(timestamp,message);
 */
```
