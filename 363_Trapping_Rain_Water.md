# Trapping Rain Water
Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it is able to trap after raining.

Trapping Rain Water

Example
Given [0,1,0,2,1,0,1,3,2,1,2,1], return 6.

Challenge
O(n) time and O(1) memory

O(n) time and O(n) memory is also acceptable.

## Solution
1. Two pointers.
**Complexity: Time O(n), Space O(1).**
```java
public class Solution {
    /**
     * @param heights: a list of integers
     * @return: a integer
     */
    public int trapRainWater(int[] heights) {
        // write your code here
        if(heights == null || heights.length == 0){
            return 0;
        }
        int left = 0, right = heights.length - 1, sum = 0;
        while(left < right){
            int leftElement = heights[left], rightElement = heights[right];
            if(leftElement < rightElement){
                left++;
                while(left < right && heights[left] < leftElement){
                    sum += (leftElement - heights[left]);
                    left++;
                }
            }
            else{
                right--;
                while(left < right && heights[right] < rightElement){
                    sum += (rightElement - heights[right]);
                    right--;
                }
            }
        }
        return sum;
    }
}
```
2. Dynamic Programming
**Complexity: Time O(n), Space O(n).**
```java
public class Solution {
    /**
     * @param heights: a list of integers
     * @return: a integer
     */
    public int trapRainWater(int[] heights) {
        // write your code here
        if(heights == null || heights.length == 0){
            return 0;
        }
        int n = heights.length, max = 0;
        int[] dp = new int[n];
        for(int i = 0; i < n; i++){
            dp[i] = max;
            max = Math.max(max, heights[i]);
        }
        max = 0;
        int water = 0;
        for(int i = n - 1; i >= 0; i--){
            dp[i] = Math.min(dp[i], max);
            max = Math.max(max, heights[i]);
            if(dp[i] > heights[i]){
                water += (dp[i] - heights[i]);
            }
        }
        return water;
    }
}
```
