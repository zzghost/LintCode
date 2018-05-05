# Add Strings
Given two non-negative integers num1 and num2 represented as string, return the sum of num1 and num2.

Example
```
Given num1 = "123", num2 = "45"
return "168"
```
## Solution
```java
public class Solution {
    /**
     * @param num1: a non-negative integers
     * @param num2: a non-negative integers
     * @return: return sum of num1 and num2
     */
    public String addStrings(String num1, String num2) {
        // write your code here
        StringBuilder rst = new StringBuilder();
        int n1 = num1.length(), n2 = num2.length();
        int carry = 0, i = n1 - 1, j = n2 - 1;
        while(i >= 0 || j >= 0){
            int sum = carry;
            if(i >= 0){
                sum += num1.charAt(i) - '0';
                i--;
            }
            if(j >= 0){
                sum += num2.charAt(j) - '0';
                j--;
            }
            carry = sum / 10;
            sum = sum % 10;
            rst.append(sum);
        }
        if(carry != 0){
            rst.append(carry);
        }
        return rst.reverse().toString();
    }
}
```
