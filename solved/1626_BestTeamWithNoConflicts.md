### 1626. Best Team With No Conflicts (Medium)

https://leetcode.com/problems/best-team-with-no-conflicts/description/

```
class Solution {
public:
    int findMaxScore(const vector<pair<int, int>>& ageScorePair) {
        const int n = ageScorePair.size();
        int res = 0;
        vector<int> dp(n);
        for (int i = 0; i < n; ++i) dp[i] = ageScorePair[i].second;
        for (int i = 0; i < n; ++i) {
            for (int j = i - 1; j >= 0; --j) {
                if (ageScorePair[j].second <= ageScorePair[i].second) {
                    dp[i] = max(dp[i], ageScorePair[i].second + dp[j]);
                }
            }
            res = max(res, dp[i]);
        }
        return res;
    }

    int bestTeamScore(vector<int>& scores, vector<int>& ages) {
        vector<pair<int, int>> ageScorePair;
        for (int i = 0; i < scores.size(); i++) {
            ageScorePair.push_back({ages[i], scores[i]});
        }
        sort(ageScorePair.begin(), ageScorePair.end());
        return findMaxScore(ageScorePair);
    }
};
```
