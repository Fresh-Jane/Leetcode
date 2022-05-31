### 360. Sort Transformed Array (Medium)

https://leetcode.com/problems/sort-transformed-array/

```
// The input is one sorted integer array and three params as a,b,c.
// And the output is another sorted integer array which each element can be calculated by the formula new_x equal to a times x square plus b times x plus c.
// Could I know the range of integer of inputs?

// The straightforward method is to traverse the original array with one for loop and push back the calculated new_x into the new array.
// Then sort the new array into ascending order and return. The time complexity is O(NlogN) where N is the size of original array.
// Because the for loop complexity is O(N) and sort complexity is O(NlogN). The space complexity is O(N) to save the result.

// Of course you are not looking for this brute force implementation, actually we don't use the sorted information of the original array and the property of quardratic funcitons.
// So here is my optimized solution:
// What about we use two pointers to scan from the two ends of the array. During the scanning, we will always get a smaller or greater y with respect to the value of a.
// For example, if a is greater than 0, we can compare the y value of two pointers, the bigger one is the biggest value among the left x range. 
// The time complexity is O(N) now. For we should return the new_x for each old elements, we at least should traverse them. The O(N) complexity should be the best one.

// Could I implement first and use one test case to go through my codes to explain more?

class Solution {
public:
    vector<int> sortTransformedArray(vector<int>& nums, int a, int b, int c) {
        const int n = nums.size();
        vector<int> res(n, 0);
        int i = 0, j = n-1;
        int k = a >= 0 ? n-1 : 0;
        auto f = [&a, &b, &c](const int& x){ return a * x * x + b * x + c; };
        while(i <= j) {
            if (a >= 0) res[k--] = f(nums[i]) >= f(nums[j]) ? f(nums[i++]) : f(nums[j--]);
            else res[k++] = f(nums[i]) <= f(nums[j]) ? f(nums[i++]) : f(nums[j--]);
        }
        return res;
    }
};
```
