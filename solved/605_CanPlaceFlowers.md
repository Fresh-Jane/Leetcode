### 605. Can Place Flowers (Easy)

https://leetcode.com/problems/can-place-flowers/

```
class Solution {
public:
    bool canPlaceFlowers(vector<int>& flowerbed, int n) {
        flowerbed.insert(flowerbed.begin(), 0);
        flowerbed.push_back(0);
        int sum = 0;
        for (int i = 1; i < flowerbed.size() - 1; ++i) {
             if (!flowerbed[i-1] && !flowerbed[i+1] && !flowerbed[i]) {
                 flowerbed[i] = 1;
                 sum++;
             }
        }
        return sum >= n;
    }
};
```
