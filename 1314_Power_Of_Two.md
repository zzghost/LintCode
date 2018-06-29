# Power of Two
Given an integer, write a function to determine if it is a power of two.
## Solution
Count each bit.The valid number only has one `1` bit.  
```java
public class Solution {
    /**
     * @param n: an integer
     * @return: if n is a power of two
     */
    public boolean isPowerOfTwo(int n) {
        // Write your code here
        int count = 0;
        while(n != 0){
            count += n & 1;
            if(count > 1){
                return false;
            }
            n = n >> 1;
        }
        return (count == 1);
    }
}
```
