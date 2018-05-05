# Merge K Sorted Interval Lists

Merge K sorted interval lists into one sorted interval list. You need to merge overlapping intervals too.

Example
Given
```
[
  [(1,3),(4,7),(6,8)],
  [(1,2),(9,10)]
]
```
Return
```
[(1,3),(4,8),(9,10)]
```
## Solution
```java
/**
 * Definition of Interval:
 * public classs Interval {
 *     int start, end;
 *     Interval(int start, int end) {
 *         this.start = start;
 *         this.end = end;
 *     }
 * }
 */

public class Solution {
    /**
     * @param intervals: the given k sorted interval lists
     * @return:  the new sorted interval list
     */
    public boolean hasIntersection(Interval i1, Interval i2){
        return ((i1.end >= i2.start && i1.end <= i2.end) ||
        (i2.start >= i1.start && i2.start <= i1.end));
    }
    public List<Interval> mergeKSortedIntervalLists(List<List<Interval>> intervals) {
        // write your code here
        PriorityQueue<Interval> pq = new PriorityQueue<>((a, b) -> (a.start - b.start));
        List<Interval> rst = new ArrayList<>();
        int row = intervals.size();
        for(int i = 0; i < row; i++){
            for(int j = 0; j < intervals.get(i).size(); j++){
                pq.offer(intervals.get(i).get(j));
            }
        }
        while(!pq.isEmpty()){
            Interval top = pq.poll();
            if(pq.isEmpty()){
                rst.add(top);
                break;
            }
            else{
                Interval senior = pq.poll();
                if(hasIntersection(top, senior)){
                  //merge two intervals.
                    top.start = Math.min(top.start, senior.start);
                    top.end = Math.max(top.end, senior.end);
                    pq.offer(top);
                }
                else{
                    rst.add(top);
                    pq.offer(senior);
                }
            }
        }
        return rst;
    }
}
```
