# Regular Expression Matching
Implement regular expression matching with support for ``'.'`` and ``'*'``.

``'.'`` Matches any single character.
``'*'`` Matches zero or more of the preceding element.
The matching should cover the entire input string (not partial).


The function prototype should be:

bool isMatch(string s, string p)

**Example**  
```
isMatch("aa","a") → false
isMatch("aa","aa") → true
isMatch("aaa","aa") → false
isMatch("aa", "a*") → true
isMatch("aa", ".*") → true
isMatch("ab", ".*") → true
isMatch("aab", "c*a*b") → true
```
## Solution
**Complexity: Time O(mn), Space O(mn)**
```java
public class Solution {
    public boolean isMatch(String s, String p) {
        // write your code here
        int m = s.length(), n = p.length();
        boolean[][] dp = new boolean[m + 1][n + 1];
        // (s== p == null) -> true and (s != null && p==null)-> false
        dp[0][0] = true;
        // (s == null && check if p matches empty)(true when p.length must be >=2)
        for(int j = 1; j <= n; j++){
            dp[0][j] = (j > 1) && ('*' == p.charAt(j - 1)) && (dp[0][j - 2]);
        }

        for(int i = 1; i <= m; i++){
            for(int j = 1; j <= n; j++){
                if(p.charAt(j - 1) == '*'){
                    dp[i][j] = j > 1 && ((s.charAt(i - 1) == p.charAt(j - 2) || p.charAt(j - 2) == '.') && dp[i - 1][j] || dp[i][j - 2]);
                }
                else{
                    dp[i][j] = dp[i - 1][j - 1] && (s.charAt(i - 1) == p.charAt(j - 1) || p.charAt(j - 1) == '.');
                }
            }
        }
        return dp[m][n];
    }
}
```
