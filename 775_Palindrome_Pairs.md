# Palindrome Pairs
Given a list of unique words, find all pairs of** distinct** indices (i, j) in the given list, so that the concatenation of the two words, i.e. words[i] + words[j] is a palindrome.

**Example**  
Given words = ``["bat", "tab", "cat"]``  
Return ``[[0, 1], [1, 0]]``  
The palindromes are ``["battab", "tabbat"]``  

Given words = ``["abcd", "dcba", "lls", "s", "sssll"]``
Return ``[[0, 1], [1, 0], [3, 2], [2, 4]]``    
The palindromes are ``["dcbaabcd", "abcddcba", "slls", "llssssll"]``

## Solution
HashMap.  
Consider 4 situations:  
1)word1 = "", find a palindrome word in the list.    
2)word1 = reverse(word2), palindrome pairs.  
3)word1 = reverse(word2.substring(word1.length, word2.length)) and word2.substring(0, word1.length) is palindrome.  
4)word1 = reverse(word2.substring(0, word1.length)) and word2.substring(word1.length, word2.length) is palindrome.
```java
public class Solution {
    /**
     * @param words: a list of unique words
     * @return: all pairs of distinct indices
     */
    public String reverse(String str){
        StringBuilder sb = new StringBuilder();
        return sb.append(str).reverse().toString();
    }
    public boolean isPalindrome(String word){
        int n = word.length();
        for(int i = 0; i < n / 2; i++){
            if(word.charAt(i) != word.charAt(n - 1 - i)){
                return false;
            }
        }
        return true;
    }
    public List<List<Integer>> palindromePairs(String[] words) {
        // Write your code here
        List<List<Integer>> rst = new ArrayList<>();
        if(words == null || words.length == 0){
            return rst;
        }
        HashMap<String, Integer> map = new HashMap<>();
        for(int i = 0; i < words.length; i++){
            map.put(words[i], i);
        }
        //"" with palindrom string.
        if(map.containsKey("")){
            for(int i = 0; i < words.length; i++){
                if(isPalindrome(words[i]) && map.get("") != i){
                    rst.add(Arrays.asList(i, map.get("")));
                    rst.add(Arrays.asList(map.get(""), i));
                }
            }
        }
        //palindrom pairs with the same length
        for(int i = 0; i < words.length; i++){
            //one situation
            String rev = reverse(words[i]);
            if(map.containsKey(rev) && map.get(rev) != i){
                rst.add(Arrays.asList(i, map.get(rev)));
            }
        }
        //palindrom pairs with substring
        for(int i = 0; i < words.length; i++){
            String w1 = words[i];
            int len = w1.length();
            for(int j = 1; j < len; j++){
                String subPre = w1.substring(0, j), subPro = w1.substring(j, len);
                if(isPalindrome(subPre)){
                    String rev = reverse(subPro);
                    if(map.containsKey(rev) && map.get(rev) != i){
                        rst.add(Arrays.asList(map.get(rev), i));
                    }
                }
                if(isPalindrome(subPro)){
                    String rev = reverse(subPre);
                    if(map.containsKey(rev) && map.get(rev) != i){
                        rst.add(Arrays.asList(i, map.get(rev)));
                    }
                }
            }
        }
        return rst;
    }
}
```
