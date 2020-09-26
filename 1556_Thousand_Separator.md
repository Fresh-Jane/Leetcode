### 1556. Thousand Separator (Easy)

Given an integer n, add a dot (".") as the thousands separator and return it in string format.


Example 1:

```
Input: n = 987
Output: "987"
```
Example 2:

```
Input: n = 1234
Output: "1.234"
```
Example 3:

```
Input: n = 123456789
Output: "123.456.789"
```
Example 4:

```
Input: n = 0
Output: "0"
```

Constraints:

- 0 <= n < 2^31

```
// Can't /1000 for one time for we should convert 020 -> "020" not "20"
class Solution {
public:
    string thousandSeparator(int n) {
        if (!n) return "0";
        string res;
        int i = 0;
        while(n) {
            int cur = n % 10;
            i++;
            n = n / 10;
            res = to_string(cur) + res;
            if (n && i % 3 == 0) res = "." + res;
        }
        return res;
    }
};
```
