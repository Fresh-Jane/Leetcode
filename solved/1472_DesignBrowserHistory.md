### 1472. Design Browser History (Medium)

https://leetcode.com/problems/design-browser-history/description/

```
class BrowserHistory {
private:
    vector<string> history;
    int size, index;
public:
    BrowserHistory(string homepage) {
        history.push_back(homepage);
        size = 1;
        index = 0;
    }
    
    void visit(string url) {
        ++index;
        if (index == history.size()) {
            history.push_back(url);
            size++;
        } else {
            history[index] = url;
            size = index + 1;
        }
    }
    
    string back(int steps) {
        index -= min(steps, index);
        return history[index];
    }
    
    string forward(int steps) {
        index += min(steps, size-index-1);
        return history[index];
    }
};

/**
 * Your BrowserHistory object will be instantiated and called as such:
 * BrowserHistory* obj = new BrowserHistory(homepage);
 * obj->visit(url);
 * string param_2 = obj->back(steps);
 * string param_3 = obj->forward(steps);
 */
```
