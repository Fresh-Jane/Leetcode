### 552. Student Attendance Record II (Hard)

Given an integer n, return the number of all possible attendance records with length n, which will be regarded as rewardable. The answer may be very large, return it modulo 109 + 7.

A student attendance record is a string that only contains the following three characters:

- 'A': Absent.
- 'L': Late.
- 'P': Present.

A record is regarded as rewardable if it does not contain more than one 'A' (absent) or more than two consecutive 'L' (late).

Example 1:

```
Input: n = 2
Output: 8
Explanation: There are 8 records with length 2 will be regarded as rewardable:
"PP" , "AP", "PA", "LP", "PL", "AL", "LA", "LL"
Only "AA" won't be regarded as rewardable owing to more than one absent time.
```

Example 2:

```
Input: n = 1
Output: 3
```

Example 3:

```
Input: n = 10101
Output: 183236316
``` 

Constraints:

- 1 <= n <= 10^5

```
// DP: https://leetcode.com/problems/student-attendance-record-ii/discuss/101643/Share-my-O(n)-C%2B%2B-DP-solution-with-thinking-process-and-explanation
// Time: O(n)
// Space: O(n)
class Solution {
public:
    int checkRecord(int n) {
        const int m = 1000000007;
        int *A = new int [n];
        int *P = new int [n];
        int *L = new int [n];
        if (n == 1) return 3;
        if (n == 2) return 8;
        P[0] = 1;
        L[0] = 1;
        L[1] = 3;
        A[0] = 1;
        A[1] = 2;
        A[2] = 4;
        for(int i = 1; i < n; i++) {
            A[i - 1] %= m;
            P[i - 1] %= m;
            L[i - 1] %= m;
            P[i] = ((A[i - 1] + P[i - 1]) % m + L[i - 1]) % m;
            if(i > 1) L[i] = ((A[i - 1] + P[i - 1]) % m + (A[i - 2] + P[i - 2]) % m) % m;
            if(i > 2) A[i] = ((A[i - 1] + A[i - 2]) % m + A[i - 3]) % m;
        }
        return ((A[n - 1] % m + P[n - 1] % m) % m + L[n - 1] % m) % m;
    }
};
```
