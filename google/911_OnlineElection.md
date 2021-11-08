### 911. Online Election (Medium)

https://leetcode.com/problems/online-election/

```
class TopVotedCandidate {
public:
    TopVotedCandidate(vector<int>& persons, vector<int>& times) {
        const int n = times.size();
        unordered_map<int, int> count;
        top_.reserve(n);
        this->times_ = times;
        int lead = -1;
        for (int i = 0; i < n; ++i) {
            lead = ++count[persons[i]] >= count[lead] ? persons[i] : lead;
            top_.push_back(lead);
        }
    }
    
    int q(int t) {
        const int index = upper_bound(times_.begin(), times_.end(), t) - times_.begin() - 1;
        return top_[index];
    }
private:
    vector<int> times_, top_;  
};

/**
 * Your TopVotedCandidate object will be instantiated and called as such:
 * TopVotedCandidate* obj = new TopVotedCandidate(persons, times);
 * int param_1 = obj->q(t);
 */
```
