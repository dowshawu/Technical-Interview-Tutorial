# Pow(x,n)

[Leetcode](https://leetcode.com/problems/powx-n/)

題意：

Implement pow(x, n). $$x^n$$


解題思路：

```java
public class Solution {
    public double myPow(double x, int n) {
        double res = 1.0;
        int pow = n;
        if (n < 0) {
            pow = -n; //轉為正的來處理
            x = 1.0 / x;
        }
        
        while (pow > 0) {
            if (pow % 2 == 1){
                res *= x;
            }
            x *= x;
            pow = pow >> 1;
        }
        
        return res;
    }
}
```