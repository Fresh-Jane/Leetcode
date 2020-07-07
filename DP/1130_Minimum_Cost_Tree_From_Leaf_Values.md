### 1130. Minimum Cost Tree From Leaf Values (M)

Given an array ```arr``` of positive integers, consider all binary trees such that:

- Each node has either 0 or 2 children;
- The values of ```arr``` correspond to the values of each **leaf** in an in-order traversal of the tree.  *(Recall that a node is a leaf if and only if it has 0 children.)*
- The value of each non-leaf node is equal to the product of the largest leaf value in its left and right subtree respectively.

Among all possible binary trees considered, return the smallest possible sum of the values of each non-leaf node.  It is guaranteed this sum fits into a 32-bit integer.

 
Example 1:

```
Input: arr = [6,2,4]
Output: 32
Explanation:
There are two possible trees.  The first has non-leaf node sum 36, and the second has non-leaf node sum 32.

    24            24
   /  \          /  \
  12   4        6    8
 /  \               / \
6    2             2   4
```

Constraints:

```
2 <= arr.length <= 40
1 <= arr[i] <= 15
It is guaranteed that the answer fits into a 32-bit signed integer (ie. it is less than 2^31).
```
```
class Solution {
public:
    vector<int> subMctFromLeafValues(vector<int>& arr, int l, int r) {
        if (l == r) {
            return {0, arr[l]};
        }
        if (r - l == 1) {
            return {arr[l] * arr[r], max(arr[l], arr[r])};
        }
        int min_sum = INT_MAX;
        int max_leaf = 0;
        for (int i = l; i < r; ++i) {
            const vector<int> res_l = subMctFromLeafValues(arr, l, i);
            const vector<int> res_r = subMctFromLeafValues(arr, i + 1, r);
            min_sum = min(min_sum, res_l[0] + res_r[0] + res_l[1] * res_r[1]); 
            max_leaf = max(max_leaf, max(res_l[1], res_r[1]));
        }
        return {min_sum, max_leaf};
    }
    int mctFromLeafValues(vector<int>& arr) {
        return subMctFromLeafValues(arr, 0, arr.size() - 1)[0];
    }
};
```