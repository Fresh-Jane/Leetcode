### 855. Exam Room (Medium)

https://leetcode.com/problems/exam-room/

```
class ExamRoom {
public:
    ExamRoom(int n) {
        N = n;
    }
    // Time: O(N)
    int seat() {
        if (L.empty()) {
            L.push_back(0);
            return 0;
        }
        int d = max(L[0], N - 1 - L[L.size() - 1]);
        for (int i = 0; i < L.size() - 1; ++i) d = max(d, (L[i+1] - L[i]) / 2);
        if (L[0] == d) {
            L.insert(L.begin(), 0);
            return 0;
        }
        for (int i = 0; i < L.size() - 1; ++i) {
            if ((L[i+1] - L[i]) / 2 == d) {
                L.insert(L.begin()+i+1, (L[i+1] + L[i]) / 2);
                return L[i+1];
            }
        }
        L.push_back(N-1);
        return N - 1;
    }
    // Time: O(N)
    void leave(int p) {
        for (int i = 0; i < L.size(); ++i) if (L[i] == p) L.erase(L.begin() + i);
    }
private:
    int N;
    vector<int> L;
};

/**
 * Your ExamRoom object will be instantiated and called as such:
 * ExamRoom* obj = new ExamRoom(n);
 * int param_1 = obj->seat();
 * obj->leave(p);
 */
```
