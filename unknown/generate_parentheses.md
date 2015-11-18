# Generate Parentheses

[Leetcode](https://leetcode.com/problems/generate-parentheses/)

題意：

Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

For example, given n = 3, a solution set is:

"((()))", "(()())", "(())()", "()(())", "()()()"

解題思路：

用DFS去作，程式碼如下：

```java
public class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> res = new ArrayList<String>();
        if (n == 0) {
            return res;
        }
        
        helper(res, n, n, new String());
        return res;
    }
    
    private void helper(List<String> res, int left, int right, String str) {
        if (left < right) {
            return;
        }
        
        if (left == 0 && right == 0) {
            res.add(new String(str));
        }
        if (left > 0) {
            helper(res, left - 1, right, str + ")");
        }
        if (right > 0) {
            helper(res, left, right - 1, str + "(");
        }
    }
}
```