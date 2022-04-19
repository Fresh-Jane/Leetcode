### 857. Minimum Cost to Hire K Workers (Hard)

https://leetcode.com/problems/minimum-cost-to-hire-k-workers/

```
class Solution {
public:
    double mincostToHireWorkers(vector<int>& quality, vector<int>& wage, int k) {
        const int n = quality.size();
        vector<E> all;
        for (int i = 0; i < n; ++i) all.emplace_back(quality[i], wage[i]);
        sort(all.begin(), all.end());
        priority_queue<double> q;
        int psum = 0;
        double res = DBL_MAX;
        for (const E& e : all) {
            q.push(e.q);
            psum += e.q;
            if (q.size() > k) {
                psum -= q.top();
                q.pop();
            }
            if (q.size() == k) {
                res = std::min(res, e.v * psum);
            }
        }
        return res;
    }
private:
    struct E {
        int q;
        double v;
        E(int q_, int w_) : q(q_), v(w_ * 1.0 / q_) {}
        bool operator<(const E& e) const {
            return v < e.v;
        }
    };
};
```
