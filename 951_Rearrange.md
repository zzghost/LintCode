# Rearrange
Given an array required to be rearranged, which means all the numbers on the even-numbered bits are less than those on the odd-numbered bits. At the same time, the even-numbered bits are sorted in ascending order, and the odd-numbered bits are also sorted in ascending order.

Example  
Given array = [-1,0,1,-1,5,10], return [-1,1,-1,5,0,10].
```
Explanation:
[-1,1,-1,5,0,10] meets the requirements.
```
Given array = [2,0,1,-1,5,10], return [-1,2,0,5,1,10].
```
Explanation:
[-1,2,0,5,1,10] meets the requirements.
```
## Solution
**Complexity: Time O(nlogn), Space O(n).**  
```java
public class Solution {
    /**
     * @param nums: the num arrays
     * @return: the num arrays after rearranging
     */
    public int[] rearrange(int[] nums) {
        // Write your code here
        Arrays.sort(nums);
        int n = nums.length;
        int[] tmp = new int[n];
        tmp = Arrays.copyOf(nums, n);
        int end = n - 1;
        for(int i = n - 1; i >= 0; i--){
            if(i % 2 != 0){
                nums[i] = tmp[end--];
            }
        }
        for(int i = n - 1; i >= 0; i--){
            if(i % 2 == 0){
                nums[i] = tmp[end--];
            }
        }
        return nums;
    }
}
```
