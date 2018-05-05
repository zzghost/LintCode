# Largest Number
## Description
Given a list of non negative integers, arrange them such that they form the largest number.

The result may be very large, so you need to return a string instead of an integer.

**Example**  
```
Given [1, 20, 23, 4, 8], the largest formed number is 8423201.
```
Challenge
Do it in O(nlogn) time complexity.

## Solution
Sort two strings.  
(s1 + s2) has the same length with (s2 + s1), so we can compare them directly.  
And we only need to override the `compare` function.
```java
public class Solution {
    /**
     * @param nums: A list of non negative integers
     * @return: A string
     */
    public class MyComparator implements Comparator{
        @Override
        public int compare(Object o1, Object o2){
            String s1 = (String)o1, s2 = (String)o2;
            return (s2 + s1).compareTo(s1 + s2);
        }
    }
    public String largestNumber(int[] nums) {
        // write your code here
        List<String> aList = new ArrayList<>();
        for(int num: nums){
            aList.add(String.valueOf(num));
        }
        MyComparator mc = new MyComparator();
        Collections.sort(aList, mc);
        StringBuilder sb = new StringBuilder();
        for(String str: aList){
            sb.append(str);
        }
        String rst = sb.toString();
        if(rst.indexOf("0") == 0){
            return "0";
        }
        return rst;
    }
}
```
