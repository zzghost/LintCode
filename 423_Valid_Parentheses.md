# Valid Parentheses
Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

**Example**  
The brackets must close in the correct order, "()" and "()[]{}" are all valid but "(]" and "([)]" are not.
## Solution
Use stack to store left parentheses.  
**Complexity: Time O(n), Space O(n).**  
```java
public class Solution {
    /**
     * @param s: A string
     * @return: whether the string is a valid parentheses
     */
    public boolean isValidParentheses(String s) {
        // write your code here
        Stack<Character> stack = new Stack<>();
        int n = s.length();
        for(Character c : s.toCharArray()){
            if(c == '(' || c == '{' || c == '['){
                stack.push(c);
            }
            else{
                if(stack.isEmpty()){
                    return false;
                }
                char tmp = stack.pop();
                if(c == ')' && tmp != '(' ||
                c == '}' && tmp != '{'||
                c == ']' && tmp != '['){
                    return false;
                }
            }
        }
        return stack.isEmpty();
    }
}
```
