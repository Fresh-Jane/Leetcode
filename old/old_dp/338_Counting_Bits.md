### 338. Counting Bits (Medium)

Given a non negative integer number num. For every numbers i in the range 0 ≤ i ≤ num calculate the number of 1's in their binary representation and return them as an array.

Example 1:

```
Input: 2
Output: [0,1,1]
```
Example 2:

```
Input: 5
Output: [0,1,1,2,1,2]
```
Follow up:

```
It is very easy to come up with a solution with run time O(n*sizeof(integer)). But can you do it in linear time O(n) /possibly in a single pass?
Space complexity should be O(n).
Can you do it like a boss? Do it without using any builtin function like __builtin_popcount in c++ or in any other language.
```
```
// Time: O(n), Space: O(n)
class Solution 1 {
public:
    vector<int> countBits(int num) {
        vector<int> res(num + 1, 0);
        for (int i = 1; i <= num; ++i) {
            res[i] = res[i & (i - 1)] + 1;
        }
        return res;
    }
};

// Time: O(n), Space: O(n)
class Solution 2 {
public:
    vector<int> countBits(int num) {
        vector<int> res(num + 1, 0);
        if (num == 0) return res;
        int i_2 = 0;
        for (int i = 1; i <= num; ++i) {
            if (i == pow(2, i_2 + 1)) i_2++;
            res[i] = res[i - pow(2, i_2)] + 1;
        }
        return res;
    }
};

// Time: O(n), Space: O(n)
class Solution 3 {
public:
    vector<int> countBits(int num) {
        vector<int> res(num + 1, 0);
        if (num == 0) return res;
        int offset = 1;
        for (int i = 1; i <= num; ++i) {
            if (offset * 2 == i) offset *= 2;
            res[i] = res[i - offset] + 1;
        }
        return res;
    }
};
```
