### 818. Race Car (Hard)

https://leetcode.com/problems/race-car/

```
// BFS with simple stl
class Solution {
public:
    int racecar(int target) {
        if (target == 0) return 0;
        unordered_map<int, unordered_set<int>> visit;
        queue<pair<int, int>> q;
        q.push({0, 1});
        int level = 0;
        while(!q.empty()) {
            int len = q.size();
            while(len--) {
                auto [pos, speed] = q.front(); q.pop();
                // A
                int ap = pos + speed;
                int as = speed * 2;
                if (ap == target) return level + 1;
                if (ap > 0 && ap < target * 2 &&
                    (!visit.count(ap) || !(visit.at(ap).count(as)))) {
                    q.push({ap, as});
                    visit[ap].insert(as);
                }
                // R
                int rp = pos;
                int rs = speed > 0 ? -1 : 1;
                if (rp > 0 && rp < target * 2 &&
                    (!visit.count(rp) || !(visit.at(rp).count(rs)))) {
                    q.push({rp, rs});
                    visit[rp].insert(rs);
                }
            }
            level++;
        }
        return -1;
    }
};

// BFS
class Solution {
public:
    struct S {
        int pos, speed;
    };
    struct Shash {
        size_t operator() (const S& s) const {
            return hash<int>()(s.pos) ^ hash<int>()(s.speed);
        }
    };
    struct Sequal {
        bool operator() (const S& s1, const S& s2) const {
            return s1.pos == s2.pos && s1.speed == s2.speed;
        }
    };
    
    int racecar(int target) {
        queue<S> q;
        q.push({0, 1});
        int res = 0;
        unordered_set<S, Shash, Sequal> visit(8, Shash(), Sequal());
        while(!q.empty()) {
            int len = q.size();
            while(len--) {
                auto cur = q.front(); q.pop();
                if (cur.pos == target) return res;
                
                S s1({cur.pos+cur.speed, cur.speed*2});
                if (s1.pos > 0 && s1.pos < target*2 && !visit.count(s1)) {
                    visit.insert(s1);
                    q.push(s1);
                }
                
                S s2({cur.pos, cur.speed > 0 ? -1 : 1});
                if (s2.pos > 0 && s2.pos < target*2 && !visit.count(s2)) {
                    visit.insert(s2);
                    q.push(s2);
                }
            }
            res++;
        }
        return -1;
    }
};
```
