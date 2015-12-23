#Sqrt(x)

[Leetcode](https://leetcode.com/problems/sqrtx/)

題意：

Implement int sqrt(int x).

Compute and return the square root of x.


解題思路：

用二分法來作，不斷的驗證 mid * mid 是否等於 x，由於 mid * mid 可能會溢位，所以我們移項改驗證 mid 是否等於 x / mid，其程式碼如下：

```java
public class Solution {
    public int mySqrt(int x) {
        if (x <= 0) {
            return x;
        }
        
        int l = 1;
        int r = x;
        int res = 1;
        
        while (l < r) {
            int mid = l + (r - l) / 2;
            if (mid > x / mid) {
                r = mid;
            } else {
                res = mid;
                l = mid + 1;
            }
        }
        
        return res;
        
    }
}
```

updated on 2015.12.23

遞迴作法，會超時

```java
public class Solution {
    public double myPow(double x, int n) {
        if (x == 0) {
            return 0;
        }
        if (n == 0) {
            return 1.0;
        }
        if (n % 2 == 0) {
            return myPow(x, n / 2) * myPow(x, n / 2);
        } else {
            return myPow(x, n / 2) * myPow(x, n / 2) * x;
        }
    }
}
```