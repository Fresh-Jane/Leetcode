### 1296. Divide Array in Sets of K Consecutive Numbers (Medium)

Given an array of integers nums and a positive integer k, find whether it's possible to divide this array into sets of k consecutive numbers
Return True if it is possible. Otherwise, return False.

Example 1:

```
Input: nums = [1,2,3,3,4,4,5,6], k = 4
Output: true
Explanation: Array can be divided into [1,2,3,4] and [3,4,5,6].
```
Example 2:

```
Input: nums = [3,2,1,2,3,4,3,4,5,9,10,11], k = 3
Output: true
Explanation: Array can be divided into [1,2,3] , [2,3,4] , [3,4,5] and [9,10,11].
```
Example 3:

```
Input: nums = [3,3,2,2,1,1], k = 3
Output: true
```
Example 4:

```
Input: nums = [1,2,3,4], k = 3
Output: false
Explanation: Each array should be divided in subarrays of size 3.
```

Constraints:

- 1 <= k <= nums.length <= 10^5
- 1 <= nums[i] <= 10^9
 

Note: This question is the same as 846: https://leetcode.com/problems/hand-of-straights/

```
class Solution {
public:
    bool isPossibleDivide(vector<int> A, int k) {
        const int n = A.size();
        if (n % k) return false;
        sort(A.begin(), A.end());
        unordered_map<int, int> c;
        for (int i : A) c[i]++;
        for (int i : A) {
            if (c.count(i) == 0 || c[i] == 0) continue;
            for (int j = k - 1; j >= 0; --j) {
                if (c.count(i+j) == 0 || c[i+j] < c[i]) return false;
                c[i+j] -= c[i];
            }
        }
        return true;
    }
};
```
