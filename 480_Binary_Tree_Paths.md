# Binary Tree Paths
Given a binary tree, return all root-to-leaf paths.

## Example  
Given the following binary tree:
```
   1
 /   \
2     3
 \
  5
  ```
All root-to-leaf paths are:
```
[
  "1->2->5",
  "1->3"
]
```

## Solution
Backtracking.  
```java
/**
 * Definition of TreeNode:
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left, right;
 *     public TreeNode(int val) {
 *         this.val = val;
 *         this.left = this.right = null;
 *     }
 * }
 */

public class Solution {
    /**
     * @param root: the root of the binary tree
     * @return: all root-to-leaf paths
     */
    List<String> paths = new ArrayList<>();
    public void DFS(TreeNode root, List<String> path){
        path.add(String.valueOf(root.val));
        if(root.left == null && root.right == null){
            List<String> tmpList = new ArrayList<>(path);
            paths.add(String.join("->", tmpList));
            path.remove(path.size() - 1);
            return ;
        }
        if(root.left != null){
            DFS(root.left, path);
        }
        if(root.right != null){
            DFS(root.right, path);
        }
        path.remove(path.size() - 1);
    }
    public List<String> binaryTreePaths(TreeNode root) {
        // write your code here
        List<String> path = new ArrayList<>();
        if(root == null){
            return paths;
        }
        DFS(root, path);
        return paths;
    }
}
```
