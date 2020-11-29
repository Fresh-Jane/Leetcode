### 934. Shortest Bridge (Medium)

In a given 2D binary array A, there are two islands.  (An island is a 4-directionally connected group of 1s not connected to any other 1s.)

Now, we may change 0s to 1s so as to connect the two islands together to form 1 island.

Return the smallest number of 0s that must be flipped.  (It is guaranteed that the answer is at least 1.)

Example 1:

```
Input: A = [[0,1],[1,0]]
Output: 1
```
Example 2:

```
Input: A = [[0,1,0],[0,0,0],[0,0,1]]
Output: 2
```
Example 3:

```
Input: A = [[1,1,1,1,1],[1,0,0,0,1],[1,0,1,0,1],[1,0,0,0,1],[1,1,1,1,1]]
Output: 1
```

Constraints:

- 2 <= A.length == A[0].length <= 100
- A[i][j] == 0 or A[i][j] == 1

```
We first paint one of the island as 2 using dfs;
Then we expand the island until we can jump to the 1st island.

class Solution {
public:
    int m,n;
    int dfs(vector<vector<int>>& A, int i, int j) {
        if (i < 0 || j < 0 || i >= m || j >= n || A[i][j] != 1) return 0;
        A[i][j] = 2;
        return 1 + dfs(A, i+1, j) + dfs(A, i-1, j) + dfs(A, i, j+1) + dfs(A, i, j-1);  
    }
    bool expand(vector<vector<int>>& A, int i, int j, int cl) {
        if (i < 0 || j < 0 || i >= m || j >= n) return false;
        if (A[i][j] == 0) A[i][j] = cl + 1;
        return A[i][j] == 1;  
    }
    
    int shortestBridge(vector<vector<int>>& A) {
        m = A.size();
        n = A[0].size();
        for (int i = 0, found = 0; !found && i < m; ++i) 
            for (int j = 0; !found && j < n; ++j) found = dfs(A, i, j);
        
        for (int cl = 2; ; ++cl)
            for (int i = 0; i < m; ++i)
                for (int j = 0; j < n; ++j)
                    if (A[i][j] == cl &&
                        (expand(A, i+1, j, cl) || expand(A, i-1, j, cl) ||
                         expand(A, i, j+1, cl) || expand(A, i, j-1, cl))) return cl - 2;
        
    }
};
```
