# House Robber
You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.

Example
Given [3, 8, 4], return 8.

Challenge
O(n) time and O(1) memory.

## Solution
Dynamic Programming.  
This solution can be optimized to O(1) memory since dp[i] depends only on dp[i - 2] and dp[i - 1].  
**Complexity: Time O(n), Space O(n).**  
```java
public class Solution {
    /**
     * @param A: An array of non-negative integers
     * @return: The maximum amount of money you can rob tonight
     */
    public long houseRobber(int[] A) {
        // write your code here
        if(A == null || A.length == 0){
            return 0;
        }
        int n = A.length;
        if(n == 1){
            return A[0];
        }
        long[] dp = new long[n];
        dp[0] = A[0];
        dp[1] = Math.max(A[0], A[1]);
        for(int i = 2; i < n; i++){
            dp[i] = Math.max(A[i] + dp[i - 2], dp[i - 1]);
        }
        return dp[n - 1];
    }
}
```
