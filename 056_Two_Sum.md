# Two Sum
Given an array of integers, find two numbers such that they add up to a specific target number.

The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2. Please note that your returned answers (both index1 and index2) are zero-based.

**Example**  
```
numbers=[2, 7, 11, 15], target=9

return [0, 1]
```
**Challenge**  
Either of the following solutions are acceptable:
```
O(n) Space, O(nlogn) Time  
O(n) Space, O(n) Time  
```
## Solution
Use HashMap.  
**Complexity: Time O(n), Space O(n)**
```java
public class Solution {
    /*
     * @param numbers: An array of Integer
     * @param target: target = numbers[index1] + numbers[index2]
     * @return: [index1 + 1, index2 + 1] (index1 < index2)
     */
    public int[] twoSum(int[] numbers, int target) {
        // write your code here
        HashMap<Integer, Integer> map = new HashMap<>();
        int n = numbers.length;
        int[] indices = null;
        for(int i = 0; i < n; i++){
            if(map.containsKey(target - numbers[i])){
                indices = new int[]{map.get(target - numbers[i]), i};
                break;
            }
            map.put(numbers[i], i);
        }
        return indices;
    }
}

```
