# Single Number
Given 2*n + 1 numbers, every numbers occurs twice except one, find it.

Example
Given [1,2,2,1,3,4,3], return 4

Challenge
One-pass, constant extra space.

## Solution
Exclusive Or.  
**Complexity: Time O(n), Space O(1).**  
```java
public class Solution {
    /**
     * @param A: An integer array
     * @return: An integer
     */
    public int singleNumber(int[] A) {
        // write your code here
        int rst = 0;
        for(int a: A){
            rst ^= a;
        }
        return rst;
    }
}
```
