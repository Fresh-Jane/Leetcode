### 341. Flatten Nested List Iterator (Medium)

https://leetcode.com/problems/flatten-nested-list-iterator/

```
/**
 * // This is the interface that allows for creating nested lists.
 * // You should not implement it, or speculate about its implementation
 * class NestedInteger {
 *   public:
 *     // Return true if this NestedInteger holds a single integer, rather than a nested list.
 *     bool isInteger() const;
 *
 *     // Return the single integer that this NestedInteger holds, if it holds a single integer
 *     // The result is undefined if this NestedInteger holds a nested list
 *     int getInteger() const;
 *
 *     // Return the nested list that this NestedInteger holds, if it holds a nested list
 *     // The result is undefined if this NestedInteger holds a single integer
 *     const vector<NestedInteger> &getList() const;
 * };
 */

class NestedIterator {
public:
    NestedIterator(vector<NestedInteger> &nestedList) {
        s.push({nestedList.begin(), nestedList.end()});
    }
    
    int next() {
        if (hasNext()) {
            int res = s.top().first->getInteger();
            ++s.top().first;
            return res;
        }
        return -1;
    }
    
    bool hasNext() {
        while (!s.empty()) {
            if (s.top().first == s.top().second) s.pop();
            else {
                if (s.top().first->isInteger()) return true;
                const auto& l = s.top().first->getList();
                ++s.top().first;
                s.push({l.begin(), l.end()});
            }
        }
        return false;
    }
private:
    using S = vector<NestedInteger>::const_iterator;
    stack<pair<S, S>> s;
};

/**
 * Your NestedIterator object will be instantiated and called as such:
 * NestedIterator i(nestedList);
 * while (i.hasNext()) cout << i.next();
 */
```
