### 990. Satisfiability of Equality Equations (Medium)

https://leetcode.com/problems/satisfiability-of-equality-equations/description/

```
class Solution {
public:
    vector<int> parent;
    int findParent(int a) {
        if (parent[a] != a) parent[a] = findParent(parent[a]);
        return parent[a];
    }

    void unionFind(int a, int b) {
        int pa = findParent(a), pb = findParent(b);
        if (pa != pb) parent[pa] = pb;
    }
    
    bool equationsPossible(vector<string>& equations) {
        for (int i = 0; i < 26; ++i) parent.push_back(i);
        for (const string& eq : equations) 
            if (eq[1] == '=') unionFind(eq[0]-'a', eq[3]-'a');
        for (const string& eq : equations)
            if (eq[1] == '!' && findParent(eq[0]-'a') == findParent(eq[3]-'a')) return false;
        return true;
    }
};
```
