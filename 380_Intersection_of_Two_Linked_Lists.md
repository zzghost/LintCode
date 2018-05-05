# Intersection of Two Linked Lists
Write a program to find the node at which the intersection of two singly linked lists begins.

Example
The following two linked lists:
```
A:          a1 → a2
                   ↘
                     c1 → c2 → c3
                   ↗            
B:     b1 → b2 → b3
```
begin to intersect at node c1.

Challenge
Your code should preferably run in O(n) time and use only O(1) memory.

## Solution
```java
/**
 * Definition for singly-linked list.
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
    /*
     * @param headA: the first list
     * @param headB: the second list
     * @return: a ListNode
     */
    public int countLength(ListNode p){
        int len = 0;
        while(p != null){
            len++;
            p = p.next;
        }
        return len;
    }
    public ListNode goFirst(ListNode p, int count){
        while(count != 0 && p != null){
            count--;
            p = p.next;
        }
        return p;
    }
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        // write your code here
        int lenA = countLength(headA), lenB = countLength(headB);
        int count = Math.abs(lenA - lenB);
        ListNode pA = headA, pB = headB;
        if(lenA >= lenB){
            pA = goFirst(pA, count);
        }
        else{
            pB = goFirst(pB, count);
        }
        while(pA != null && pB != null){
            if(pA == pB){
                return pA;
            }
            pA = pA.next;
            pB = pB.next;
        }
        return null;
    }
}
```
