# Digital Problem
Give a conversion rule to convert number n：

n is an odd number: n = 3 * n + 1
n is an even number: n = n / 2
After several conversions, n will become 1.
Given a number n, find the times of converting to 1.

Example
Given n = 2, return 1.

Explanation:
```
2→1
```
Given n = 3, return 7.

Explanation:
```
3→10→5→16→8→4→2→1
```
## Solution
Simulation.  
```java
public class Solution {
    /**
     * @param n: the number n
     * @return: the times n convert to 1
     */
    public int digitConvert(int n) {
        // Write your code here
        int step = 0;
        while(n != 1){
            if(n % 2 == 0){
                n = n / 2;
            }
            else{
                n = 3 * n + 1;
            }
            step++;
        }
        return step;
    }
}
```
