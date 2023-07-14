### 399. Evaluate Division (Medium)

https://leetcode.com/problems/evaluate-division/description/

```
// Union find
class Solution {
private:
    struct Node {
        Node* parent;
        double value = 0.0;
        Node() : parent(this) {}
    };

    Node* findParent(Node* n) {
        if (n->parent != n)
            n->parent = findParent(n->parent);
        return n->parent;
    }
    
    void unionSet(Node* n1, Node* n2, double value, map<string, Node*>& m) {
        Node* p1 = findParent(n1), *p2 = findParent(n2);
        double ratio = n2->value * value / n1->value;
        for (auto it = m.begin(); it != m.end(); ++it) 
            if (findParent(it->second) == p1)
                it->second->value *= ratio;
        p1->parent = p2;
    }

public:
    vector<double> calcEquation(vector<vector<string>>& equations, vector<double>& values, vector<vector<string>>& queries) {
        map<string, Node*> m;
        for (int i = 0; i < equations.size(); ++i) {
            string a = equations[i][0], b = equations[i][1];
            if (m.count(a) == 0 && m.count(b) == 0) {
                m[a] = new Node();
                m[b] = new Node();
                m[a]->value = values[i];
                m[b]->value = 1;
                m[a]->parent = m[b];
            } else if (m.count(a) == 0) {
                m[a] = new Node();
                m[a]->value = values[i] * m[b]->value;
                m[a]->parent = m[b];
            } else if (m.count(b) == 0) {
                m[b] = new Node();
                m[b]->value = m[a]->value / values[i];
                m[b]->parent = m[a];
            } else unionSet(m[a], m[b], values[i], m);
        }
        vector<double> res;
        for (vector<string>& q : queries) {
            string qa = q[0], qb = q[1];
            if (m.count(qa) == 0 || m.count(qb) == 0 || findParent(m[qa]) != findParent(m[qb]))
                res.push_back(-1.0);
            else res.push_back(m[qa]->value / m[qb]->value);
        } 
        return res;
    }
};

// DFS
class Solution {
private:
    unordered_map<string, vector<pair<string, double>>> m;
public:
    vector<double> calcEquation(vector<vector<string>>& equations, vector<double>& values, vector<vector<string>>& queries) {
        const int n = equations.size();
        for (int i = 0; i < n; ++i) {
            const string a = equations[i][0], b = equations[i][1];
            m[a].push_back({b, values[i]});
            m[b].push_back({a, 1.0 / values[i]});
        }
        vector<double> res;
        unordered_set<string> visited;
        for (const vector<string>& q : queries) {
            const string c = q[0], d = q[1];
            double r = 1.0;
            if (!m.count(c) || !m.count(d) || !dfs(c, d, visited, r)) res.push_back(-1.0);
            else res.push_back(r);
        }
        return res;
    }
    bool dfs(const string& start, const string& end, unordered_set<string> visited, double& res) {
        if (start == end) return true;
        const vector<pair<string, double>>& all_next = m.at(start);
        visited.insert(start);
        for (const auto& p : all_next) {
            if (!visited.count(p.first)) {
                res *= p.second;
                if (dfs(p.first, end, visited, res)) return true;
                res /= p.second;
            }
        }
        return false;
    }
};
```
