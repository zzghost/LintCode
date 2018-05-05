# Flatten 2D Vector
Implement an iterator to flatten a 2d vector.

Example
Given 2d vector =
```
[
  [1,2],
  [3],
  [4,5,6]
]
```
By calling next repeatedly until hasNext returns false, the order of elements returned by next should be: [1,2,3,4,5,6].

## Solution
1. Use an array to record the vec2d.   
```java
public class Vector2D implements Iterator<Integer> {
    public int n;
    public List<Integer> nums;
    public int idx;
    public Vector2D(List<List<Integer>> vec2d) {
        // Initialize your data structure here
        nums = new ArrayList<>();
        for(int i = 0; i < vec2d.size(); i++){
            for(int j = 0; j < vec2d.get(i).size(); j++){
                nums.add(vec2d.get(i).get(j));
            }
        }
        n = nums.size();
        idx = 0;
    }

    @Override
    public Integer next() {
        // Write your code here
        return nums.get(idx++);
    }

    @Override
    public boolean hasNext() {
        // Write your code here
        return (idx < n);
    }

    @Override
    public void remove() {}
}
```
2. Record current row and col(Not so quick)
```java
public class Vector2D implements Iterator<Integer> {
    private int ROW;
    private int currRow;
    private int currCol;
    List<List<Integer>> vec = null;
    public Vector2D(List<List<Integer>> vec2d) {
        // Initialize your data structure here
        this.vec = vec2d;
        this.ROW = vec2d.size();
        this.currRow = 0;
        this.currCol = 0;
    }

    @Override
    public Integer next() {
        // Write your code here
        int num = vec.get(currRow).get(currCol);
        currCol++;
        if(currCol >= vec.get(currRow).size()){
            currRow++;
            currCol = 0;
        }
        return num;
    }

    @Override
    public boolean hasNext() {
        // Write your code here
        while(ROW > currRow){
            if(vec.get(currRow).size() == 0){
                currRow++;
                currCol = 0;
            }
            else{
                return true;
            }
        }
        return (ROW < currRow);
    }

    @Override
    public void remove() {}
}
```
