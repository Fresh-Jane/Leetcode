### 1570. Dot Product of Two Sparse Vectors (Medium)

https://leetcode.com/problems/dot-product-of-two-sparse-vectors/

```
class SparseVector {
public:
    SparseVector(vector<int> &nums) {
        for (int i = 0; i < nums.size(); ++i)
            if (nums[i] != 0) m[i] = nums[i];
    }
    // Return the dotProduct of two sparse vectors
    int dotProduct(SparseVector& vec) {
        int res = 0;
        for (auto p : vec.m) 
            if (this->m.count(p.first)) res += p.second * this->m[p.first];
        return res;
    }
private:
    unordered_map<int, int> m;
};

// Your SparseVector object will be instantiated and called as such:
// SparseVector v1(nums1);
// SparseVector v2(nums2);
// int ans = v1.dotProduct(v2);
```
