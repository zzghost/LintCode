# Merge K Sorted Lists
Merge k sorted linked lists and return it as one sorted list.

Analyze and describe its complexity.

Example  
Given lists:
```
[
  2->4->null,
  null,
  -1->null
],
```
return -1->2->4->null.

## Solution
Priority Queue.  
```java
/**
 * Definition for ListNode.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int val) {
 *         this.val = val;
 *         this.next = null;
 *     }
 * }
 */
public class Solution {
    /**
     * @param lists: a list of ListNode
     * @return: The head of one sorted list.
     */
    public ListNode mergeKLists(List<ListNode> lists) {  
        // write your code here
        if(lists == null || lists.size() == 0){
            return null;
        }
        PriorityQueue<ListNode> pq = new PriorityQueue<>(lists.size(), new Comparator<ListNode>(){
            public int compare(ListNode l1, ListNode l2){
                return l1.val - l2.val;
            }
        });
        int n = lists.size();
        for(int i = 0; i < n; i++){
            if(lists.get(i) != null){
                pq.offer(lists.get(i));
            }
        }
        ListNode head = new ListNode(0), p = head;
        while(!pq.isEmpty()){
            ListNode tmp = pq.poll();
            p.next = tmp;
            p = p.next;
            if(tmp.next != null){
                pq.offer(tmp.next);
            }
        }
        return (head.next == null) ? null : head.next;
    }
}

```
