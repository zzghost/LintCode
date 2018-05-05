# Course ScheduleIII
Description
There are ·n· different online courses numbered from 1 to n. Each course has some duration(course length) t and closed on dth day. A course should be taken continuously for t days and must be finished before or on the dth day. You will start at the 1st day.

Given n online courses represented by pairs (t,d), your task is to find the maximal number of courses that can be taken.

The integer 1 <= d, t, n <= 10,000.
You can't take two courses simultaneously.

Example  
Given [[100, 200], [200, 1300], [1000, 1250], [2000, 3200]]
return 3

There're totally 4 courses, but you can take 3 courses at most:
First, take the 1st course, it costs 100 days so you will finish it on the 100th day, and ready to take the next course on the 101st day.
Second, take the 3rd course, it costs 1000 days so you will finish it on the 1100th day, and ready to take the next course on the 1101st day.
Third, take the 2nd course, it costs 200 days so you will finish it on the 1300th day.
The 4th course cannot be taken now, since you will finish it on the 3300th day, which exceeds the closed date.
## Solution
1. Iterative  
Sort each course using its ending by ascending order.    
**Complexity: Time O(n * count), Space O(1).**
```java
public class Solution {
    /**
     * @param courses: duration and close day of each course
     * @return: the maximal number of courses that can be taken
     */
    public int scheduleCourse(int[][] courses) {
        // write your code here
        Arrays.sort(courses, (a, b) -> (a[1] - b[1]));
        int time = 0, count = 0;
        int n = courses.length;
        for(int i = 0; i < n; i++){
            if(time + courses[i][0] <= courses[i][1]){
                time += courses[i][0];
                courses[count++] = courses[i];
            }
            else{
                int maxI = i;
                //find a replacement
                for(int j = 0; j < count; j++){
                    if(courses[maxI][0] < courses[j][0]){
                        maxI = j;
                    }
                }
                if(courses[maxI][0] >= courses[i][0]){
                    time += courses[i][0] - courses[maxI][0];
                    courses[maxI] = courses[i];
                }
            }
        }
        return count;
    }
}
```
2. Using list to store results.  
Actually the same as solution 1.  
**Complexity: Time O(n * m), Space O(n).**  
```java
public class Solution {
    /**
     * @param courses: duration and close day of each course
     * @return: the maximal number of courses that can be taken
     */
    public int scheduleCourse(int[][] courses) {
        // write your code here
        Arrays.sort(courses, (a, b) -> (a[1] - b[1]));
        List<Integer> validList = new ArrayList<>();
        int time = 0;
        for(int[] c : courses){
            if(time + c[0] <= c[1]){
                validList.add(c[0]);
                time += c[0];
            }
            else{
                int maxI = 0;
                for(int i = 1; i < validList.size(); i++){
                    if(validList.get(i) > validList.get(maxI)){
                        maxI = i;
                    }
                }
                if(maxI < validList.size() && validList.get(maxI) > c[0]){
                    time += c[0] - validList.get(maxI);
                    validList.set(maxI, c[0]);
                }
            }
        }
        return validList.size();
    }
}
```
3. Using Priority Queue  
Use Priority Queue to find the maximum course which is to be replaced.  
**Complexity: O(nlogn), Space O(n).**
```java
public class Solution {
    /**
     * @param courses: duration and close day of each course
     * @return: the maximal number of courses that can be taken
     */
    public int scheduleCourse(int[][] courses) {
        // write your code here
        Arrays.sort(courses, (a, b) -> (a[1] - b[1]));
        PriorityQueue<Integer> pq = new PriorityQueue<>((a, b) -> (b - a));
        int n = courses.length, time = 0;
        for(int i = 0; i < n; i++){
            if(time + courses[i][0] <= courses[i][1]){
                time += courses[i][0];
                pq.offer(courses[i][0]);
            }
            else{
                if(!pq.isEmpty() && pq.peek() > courses[i][0]){
                    time -= pq.poll();
                    pq.offer(courses[i][0]);
                    time += courses[i][0];
                }
            }
        }
        return pq.size();
    }
}
```
