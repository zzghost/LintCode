# Word Search II
## Description
Given a matrix of lower alphabets and a dictionary. Find all words in the dictionary that can be found in the matrix. A word can start from any position in the matrix and go left/right/up/down to the adjacent position.

**Example  **  
Given matrix:
```
doaf
agai
dcan
```
and dictionary:
```
{"dog", "dad", "dgdg", "can", "again"}
```
return {"dog", "dad", "can", "again"}


dog:
```
doaf
agai
dcan
```
dad:
```
doaf
agai
dcan
```
can:
```
doaf
agai
dcan
```
again:
```
doaf
agai
dcan
```
**Challenge**  
Using trie to implement your algorithm.


## Solution
1. DFS  
DFS by word(TLE).DFS each position and check if the result is correct(TLE).  
DFS each position and check each character by word.(AC)    
```java
public class Solution {
    /**
     * @param board: A list of lists of character
     * @param words: A list of string
     * @return: A list of string
     */
    HashSet<String> dict = new HashSet<>();
    HashSet<String> wordSet = new HashSet<>();
    public boolean dfs(char[][] board, int row, int col, int idx, String target){
        if(row < 0 || col < 0 || row >= board.length || col >= board[0].length){
            return false;
        }
        if(target.charAt(idx) != board[row][col]){
            return false;
        }
        if(target.length() - 1 == idx){
            return true;
        }
        board[row][col] = '*';
        boolean rst = dfs(board, row - 1, col, idx + 1, target) || dfs(board, row + 1, col, idx + 1, target) || dfs(board, row, col - 1, idx + 1, target) || dfs(board, row, col + 1, idx + 1, target);
        board[row][col] = target.charAt(idx);
        return rst;
    }
    public List<String> wordSearchII(char[][] board, List<String> words) {
        // write your code here
        for(String str: words){
            dict.add(str);
        }
        for(int i = 0; i < board.length; i++){
            for(int j = 0; j < board[0].length; j++){
                for(String target: words){
                    if(dfs(board, i, j, 0, target)){
                        wordSet.add(target);
                    }
                }
            }
        }
        return new ArrayList<>(wordSet);
    }
}
```
2. Trie  
Turn the word dictionary into Trie tree and do dfs on the board, check if the traversal string has prefix in the Trie tree.  
```java
public class Solution {
    /**
     * @param board: A list of lists of character
     * @param words: A list of string
     * @return: A list of string
     */
    class TrieNode{
        boolean isEnd = false;
        HashMap<Character, TrieNode> map = new HashMap();
        TrieNode(){

        }
        void setKeyword(boolean end){
            isEnd = end;
        }
        boolean getKeywordEnd(){
            return isEnd;
        }
        void addSubNode(char c, TrieNode node){
            map.put(c, node);
        }
        TrieNode getSubNode(char c){
            return map.get(c);
        }
        int countSubNode(char c){
            return map.size();
        }
    }
    class Trie{
        TrieNode root = null;
        public Trie(){
            root = new TrieNode();
        }
        public void addWord(String word){
            int len = word.length();
            TrieNode node = root;
            for(int i = 0; i < len; i++){
                char c = word.charAt(i);
                TrieNode tmp = node.getSubNode(c);
                if(tmp == null){
                    tmp = new TrieNode();
                    node.addSubNode(c, tmp);
                }
                node = tmp;
                if(i == len - 1){
                    node.setKeyword(true);
                }
            }
        }
        public boolean exist(String word){
            int len = word.length();
            TrieNode node = root;
            for(int i = 0; i < len; i++){
                char c = word.charAt(i);
                TrieNode tmp = node.getSubNode(c);
                if(tmp == null){
                    return false;
                }
                node = tmp;
            }
            return node.getKeywordEnd();
        }
    }

    Trie trie = new Trie();
    HashSet<String> rst = new HashSet<>();

    public boolean dfs(char[][] board, int row, int col, String str, TrieNode node){
        if(row < 0 || col < 0 || row >= board.length || col >= board[0].length){
            return false;
        }
        if(board[row][col] == '*'){
            return false;
        }
        TrieNode tn = node.getSubNode(board[row][col]);
        if(tn == null){
            return false;
        }
        str += board[row][col];
        if(tn.getKeywordEnd()){
            rst.add(str);
        }

        char tmp = board[row][col];
        board[row][col] = '*';
        boolean rst = dfs(board, row - 1, col, str, tn) ;
        rst = dfs(board, row + 1, col, str, tn) || rst;
        rst = dfs(board, row, col - 1, str, tn) || rst;
        rst = dfs(board, row, col + 1, str, tn) || rst;
        board[row][col] = tmp;
        return rst;

    }
    public List<String> wordSearchII(char[][] board, List<String> words) {
        // write your code here
        if(board == null || board.length == 0){
            return new ArrayList<>();
        }
        int m = board.length, n = board[0].length;
        for(String str: words){
            trie.addWord(str);
        }

        for(int i = 0; i < m; i++){
            for(int j = 0; j < n; j++){
                dfs(board, i, j, "", trie.root);
            }
        }

        return new ArrayList<>(rst);
    }
}
```
