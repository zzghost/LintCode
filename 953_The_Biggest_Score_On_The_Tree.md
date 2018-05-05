# 953. The Biggest Score On The Tree
Given a multitree of n nodes, and the node numbered from 0 to n - 1, and the root numbered 0. Each node has a revenue, you can add the revenue of this node when you get to it. Each side has a cost, we will subtract the cost of this side when walking along it. Find the maximum total (total score = total return - total cost) score from the root node to any leaf node.

Example
```
Given x = [0,0,0],y = [1,2,3], cost = [1,1,1], profit = [1,1,2,3]，return 3.
Route: 0→3
```
```
Given x = [0,0],y = [1,2], cost =[1,2], profit = [1,2,5]，return 4.
Route: 0→2
```
## Solution
Depth-first search.  
Use HashMap to store the graph.  
```java
public class Solution {
    /**
     * @param x: The vertex of edge
     * @param y: The another vertex of edge
     * @param cost: The cost of edge
     * @param profit: The profit of vertex
     * @return: Return the max score
     */
    private int score = 0;
    public void dfs(HashMap<Integer, ArrayList<Integer>> tree, HashMap<Integer, Integer> edge, int[] profit, int idx, int tmpScore){

        tmpScore += profit[idx] - edge.get(idx);
        //leaf node
        if(!tree.containsKey(idx) || tree.get(idx).size() == 0){
            score = Math.max(score, tmpScore);
            tmpScore -= profit[idx] + edge.get(idx);
            return ;
        }

        for(int i = 0; i < tree.get(idx).size(); i++){
            dfs(tree, edge, profit, tree.get(idx).get(i), tmpScore);
        }
        tmpScore -= profit[idx] + edge.get(idx);
    }
    public int getMaxScore(int[] x, int[] y, int[] cost, int[] profit) {
        // Write your code here
        int n = x.length;
        HashMap<Integer, ArrayList<Integer>> tree = new HashMap<>();
        for(int i = 0; i < n; i++){
            ArrayList<Integer> aList = tree.getOrDefault(x[i], new ArrayList<Integer>());
            aList.add(y[i]);
            tree.put(x[i], aList);
        }
        HashMap<Integer, Integer> edge = new HashMap<>();
        edge.put(0, 0);
        for(int i = 0; i < n; i++){
            edge.put(y[i], cost[i]);
        }
        dfs(tree, edge, profit, 0, 0);
        return score;
    }
}
```
