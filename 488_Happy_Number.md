# Happy Number
Write an algorithm to determine if a number is happy.

A happy number is a number defined by the following process: Starting with any positive integer, replace the number by the sum of the squares of its digits, and repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1. Those numbers for which this process ends in 1 are happy numbers.

Example
19 is a happy number
```
1^2 + 9^2 = 82
8^2 + 2^2 = 68
6^2 + 8^2 = 100
1^2 + 0^2 + 0^2 = 1
```
## Solution
Use HashSet to simulate the progress.  
```java
public class Solution {
    /**
     * @param n: An integer
     * @return: true if this is a happy number or false
     */
    public boolean isHappy(int n) {
        // write your code here
        HashSet<Integer> number = new HashSet<>();
        while(n != 1){
            int sum = 0;
            int tmp = n;
            while(tmp != 0){
                int t = tmp % 10;
                sum += Math.pow(t, 2);
                tmp /= 10;
            }
            if(number.contains(sum)){
                return false;
            }
            number.add(sum);
            n = sum;
        }
        return true;
    }
}
```
