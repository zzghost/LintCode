# Sequence Reconstruction
Check whether the original sequence org can be uniquely reconstructed from the sequences in seqs. The org sequence is a permutation of the integers from 1 to n, with 1 ≤ n ≤ 10^4. Reconstruction means building a shortest common supersequence of the sequences in seqs (i.e., a shortest sequence so that all sequences in seqs are subsequences of it). Determine whether there is only one sequence that can be reconstructed from seqs and it is the org sequence.

**Example**  
```
Given org = [1,2,3], seqs = [[1,2],[1,3]]
Return false
Explanation:
[1,2,3] is not the only one sequence that can be reconstructed, because [1,3,2] is also a valid sequence that can be reconstructed.

Given org = [1,2,3], seqs = [[1,2]]
Return false
Explanation:
The reconstructed sequence can only be [1,2].

Given org = [1,2,3], seqs = [[1,2],[1,3],[2,3]]
Return true
Explanation:
The sequences [1,2], [1,3], and [2,3] can uniquely reconstruct the original sequence [1,2,3].

Given org = [4,1,5,2,6,3], seqs = [[5,2,6,3],[4,1,5,2]]
Return true
```
## Solution
Topological sort will get memory limit exeeded.  
Just check each position and mark the visited one.  
Be careful with `org=[], seqs=[[]]` and `org=[1], seqs=[[],[]]` situation.  
```java
public class Solution {
    /**
     * @param org: a permutation of the integers from 1 to n
     * @param seqs: a list of sequences
     * @return: true if it can be reconstructed only one or false
     */
    public boolean sequenceReconstruction(int[] org, int[][] seqs) {
        // write your code here
        int n = org.length;
        int[] pos = new int[n + 1];
        for(int i = 0; i < n; i++){
            pos[org[i]] = i;
        }
        int totalMatch = n - 1;
        boolean[] matched = new boolean[n + 1];
        boolean noEmpty = false;
        for(int i = 0; i < seqs.length; i++){
            int size = seqs[i].length;
            if(size > 0){
                noEmpty = true;
            }
            for(int j = 0; j < size; j++){
                if(seqs[i][j] < 1 || seqs[i][j] > n){
                    return false;
                }
                if(j == 0){
                    continue;
                }
                int pre = seqs[i][j - 1], pro = seqs[i][j];
                if(pos[pre] >= pos[pro]){
                    return false;
                }
                if(matched[pro] == false && pos[pre] + 1 == pos[pro]){
                    totalMatch--;
                    matched[pro] = true;
                }
            }
        }
        return (totalMatch == 0 && noEmpty) || (!noEmpty && n == 0);
    }
}
```
