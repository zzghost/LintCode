# Alien Dictionary
There is a new alien language which uses the latin alphabet. However, the order among letters are unknown to you. You receive a list of non-empty words from the dictionary, where words are sorted lexicographically by the rules of this new language. Derive the order of letters in this language.

Example
Given the following words in dictionary,
```
[
  "wrt",
  "wrf",
  "er",
  "ett",
  "rftt"
]
```
The correct order is: ``"wertf"``

Given the following words in dictionary,
```
[
  "z",
  "x"
]
```
The correct order is: ``"zx"``.
## Solution
Topological sort.  
Contruct the contraint conditions first(construct the graph).  
And then do Topological sort.  
```java
public class Solution {
  /**
   * @param words: a list of words
   * @return: a string which is correct order
   */
  public String alienOrder(String[] words) {
      // Write your code here
      if(words == null || words.length == 0){
          return "";
      }
      HashMap<Character, HashSet<Character>> graph = new HashMap<>();
      HashMap<Character, Integer> indegree = new HashMap<>();
      HashSet<Character> charSet = new HashSet<>();
      HashSet<Character> appearSet = new HashSet<>();
      String preWord = "";
      for(String curr : words){
          for(Character c : curr.toCharArray()){
              charSet.add(c);
          }

          for(int i = 0; i < Math.min(preWord.length(), curr.length()); ++i){
              char pre = preWord.charAt(i), pro = curr.charAt(i);
              if(pre == pro){
                continue;
              }
              //skip duplicates
              if(graph.containsKey(pre) && graph.get(pre).contains(pro)){
                continue;
              }
              if(!indegree.containsKey(pro)){
                  indegree.put(pro, 1);
              }
              else{
                  int t = indegree.get(pro);
                  indegree.put(pro, t + 1);
              }
              if(!graph.containsKey(pre)){
                  graph.put(pre, new HashSet<Character>());
              }
              appearSet.add(pre);
              appearSet.add(pro);
              graph.get(pre).add(pro);
              break;
          }
          preWord = curr;
      }
      Queue<Character> queue = new LinkedList<>();
      for(Character c : appearSet){
          if(!indegree.containsKey(c)){
              queue.offer(c);
          }
      }
      StringBuilder sb = new StringBuilder();
      while(!queue.isEmpty()){
          char top = queue.poll();
          sb.append(top);
          if(!graph.containsKey(top)){
              continue;
          }
          for(Character c : graph.get(top)){
              indegree.put(c, indegree.get(c) - 1);
              if(indegree.get(c) == 0){
                  queue.offer(c);
              }
          }
      }
      for(Character ch : charSet){
          if(indegree.containsKey(ch) && indegree.get(ch) != 0){
              return "";
          }
          if(!appearSet.contains(ch)){
              int i = 0;
              while(i < sb.length()){
                  if(sb.charAt(i) < ch){
                      i++;
                  }
                  else{
                    break;
                  }
              }
              sb.insert(i, ch);
          }
      }
      return sb.toString();
  }
}
```
