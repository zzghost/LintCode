# Same Number
Given an array, If the same number exists in the array, and the distance of the same number is less than the given value k, output YES, otherwise output NO.

## Example
Given array = [1,2,3,1,5,9,3], k = 4, return "YES".
```
Explanation:
The distance of 1 whose indexes are  3 and 0 is 3, which meets the requirement and output YES.
```
Given array =[1,2,3,5,7,1,5,1,3], k = 4, return "YES".
```
Explanation:
The distance of 1 whose indexes are  7 and 5 is 2, which meets the requirement and output YES.
```
## Solution
```java
public class Solution {
    /**
     * @param nums: the arrays
     * @param k: the distance of the same number
     * @return: the ans of this question
     */
    public String sameNumber(int[] nums, int k) {
        // Write your code here
        HashMap<Integer, Integer> map = new HashMap<>();
        int n = nums.length;
        for(int i = 0; i < n; i++){
            if(map.containsKey(nums[i])){
                if(i - map.get(nums[i]) < k){
                    return "YES";
                }
            }
            map.put(nums[i], i);
        }
        return "NO";
    }
}
```
