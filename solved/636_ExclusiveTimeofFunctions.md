### 636. Exclusive Time of Functions (Medium)

https://leetcode.com/problems/exclusive-time-of-functions/

```
class Solution {
public:
    vector<int> exclusiveTime(int n, vector<string>& logs) {
        vector<int> res(n);
        stack<pair<int, int>> st;
        for (string l : logs) {
            auto [i, start, t] = parse(l);
            if (start) {
                if (!st.empty()) res[st.top().first] += t - st.top().second;
                st.push({i, t});
            } else {
                int start_t = st.top().second;
                st.pop();
                res[i] += t - start_t + 1;
                if (!st.empty()) st.top().second = t + 1;
            }
        }
        return res;
    }
    tuple<int, int, int> parse(string log) {
        istringstream ss(log);
        string line;
        int k = 0;
        int i, t, start;
        while(getline(ss, line, ':')) {
            if (k == 0) i = stoi(line);
            else if (k == 1) start = line[0] == 's';
            else t = stoi(line);
            k++;
        }
        return {i, start, t};
    }
};
```
