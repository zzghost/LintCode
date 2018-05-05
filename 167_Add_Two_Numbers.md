# Add Two Numbers
You have two numbers represented by a linked list, where each node contains a single digit. The digits are stored in reverse order, such that the 1's digit is at the head of the list. Write a function that adds the two numbers and returns the sum as a linked list.

Example
```
Given 7->1->6 + 5->9->2. That is, 617 + 295.

Return 2->1->9. That is 912.

Given 3->1->5 and 5->9->2, return 8->0->8.
```
## Solution
```java
/**
 * Definition for ListNode
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */

public class Solution {
    /**
     * @param l1: the first list
     * @param l2: the second list
     * @return: the sum list of l1 and l2
     */
    public ListNode addLists(ListNode l1, ListNode l2) {
        // write your code here
        ListNode p1 = l1, p2 = l2;
        int carry = 0;
        while(p1 != null || p2 != null || carry != 0){
            int sum = carry;
            if(p1 != null){
                sum += p1.val;
            }
            if(p2 != null){
                sum += p2.val;
                p2 = p2.next;
            }
            p1.val = sum % 10;
            carry = sum / 10;
            //create a new node to avoid additional operations
            if(p1.next == null && (carry != 0 || p2 != null)){
                p1.next = new ListNode(0);
            }
            p1 = p1.next;
        }
        return l1;
    }
}
```
