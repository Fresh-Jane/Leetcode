### 364. Nested List Weight Sum II (Medium)

https://leetcode.com/problems/nested-list-weight-sum-ii/

```
/**
 * // This is the interface that allows for creating nested lists.
 * // You should not implement it, or speculate about its implementation
 * class NestedInteger {
 *   public:
 *     // Constructor initializes an empty nested list.
 *     NestedInteger();
 *
 *     // Constructor initializes a single integer.
 *     NestedInteger(int value);
 *
 *     // Return true if this NestedInteger holds a single integer, rather than a nested list.
 *     bool isInteger() const;
 *
 *     // Return the single integer that this NestedInteger holds, if it holds a single integer
 *     // The result is undefined if this NestedInteger holds a nested list
 *     int getInteger() const;
 *
 *     // Set this NestedInteger to hold a single integer.
 *     void setInteger(int value);
 *
 *     // Set this NestedInteger to hold a nested list and adds a nested integer to it.
 *     void add(const NestedInteger &ni);
 *
 *     // Return the nested list that this NestedInteger holds, if it holds a nested list
 *     // The result is undefined if this NestedInteger holds a single integer
 *     const vector<NestedInteger> &getList() const;
 * };
 */
// One pass dfs
// convert the equition.
class Solution {
public:
    int w_sum, sum, max_level;
    int depthSumInverse(vector<NestedInteger>& nestedList) {
        w_sum = 0, sum = 0, max_level = 1;
        dfs(nestedList, 1);
        return (max_level + 1) * sum - w_sum;
    }
    void dfs(vector<NestedInteger>& nestedList, int level) {
        for(auto n : nestedList) {
            if (n.isInteger()) {
                w_sum += level * n.getInteger();
                sum += n.getInteger();
                max_level = max(level, max_level);
            } else {
                dfs(n.getList(), level + 1);
            }
        }
    }
};
```
