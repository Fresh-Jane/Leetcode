### 1631. Path With Minimum Effort (Medium)

You are a hiker preparing for an upcoming hike. You are given heights, a 2D array of size rows x columns, where heights[row][col] represents the height of cell (row, col). You are situated in the top-left cell, (0, 0), and you hope to travel to the bottom-right cell, (rows-1, columns-1) (i.e., 0-indexed). You can move up, down, left, or right, and you wish to find a route that requires the minimum effort.

A route's effort is the maximum absolute difference in heights between two consecutive cells of the route.

Return the minimum effort required to travel from the top-left cell to the bottom-right cell.

Example 1:

```
Input: heights = [[1,2,2],[3,8,2],[5,3,5]]
Output: 2
Explanation: The route of [1,3,5,3,5] has a maximum absolute difference of 2 in consecutive cells.
This is better than the route of [1,2,2,2,5], where the maximum absolute difference is 3.
```
Example 2:

```
Input: heights = [[1,2,3],[3,8,4],[5,3,5]]
Output: 1
Explanation: The route of [1,2,3,4,5] has a maximum absolute difference of 1 in consecutive cells, which is better than route [1,3,5,3,5].
```
Example 3:

```
Input: heights = [[1,2,1,1,1],[1,2,1,2,1],[1,2,1,2,1],[1,2,1,2,1],[1,1,1,2,1]]
Output: 0
Explanation: This route does not require any effort.
```

Constraints:

- rows == heights.length
- columns == heights[i].length
- 1 <= rows, columns <= 100
- 1 <= heights[i][j] <= 10^6

```
// Dijikstra to calculate the minimum path 
// Time: O(MN log MN)
// Space: O(MN)
class Solution {
public:
    int minimumEffortPath(vector<vector<int>>& heights) {
        const vector<vector<int>> go = {{0, 1}, {0, -1}, {1, 0}, {-1, 0}};
        const int m = heights.size(), n = heights[0].size();
        vector<vector<int>> efforts(m, vector<int>(n, INT_MAX));
        priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;
        pq.emplace(0, 0);
        while (!pq.empty()) {
            const int effort = pq.top().first;
            const int x = pq.top().second / 100, y = pq.top().second % 100;
            pq.pop();
            if (x == m - 1 && y == n - 1) return effort;
            if (effort >= efforts[x][y]) continue;
            efforts[x][y] = effort;
            for (int i = 0; i < 4; ++i) {
                const int nx = x + go[i][0], ny = y + go[i][1];
                if (nx < 0 || nx >= m || ny < 0 || ny >= n) continue;
                const int cur_effort = max(effort, abs(heights[x][y] - heights[nx][ny]));
                pq.emplace(cur_effort, 100 * nx + ny);
            }
        }
        return -1;
    }
};
```
