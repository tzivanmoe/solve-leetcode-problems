# Shortest Word Distance III

This is a follow up of Shortest Word Distance. The only difference is now word1 could be the same as word2.

Given a list of words and two words word1 and word2, return the shortest distance between these two words in the list.

word1 and word2 may be the same and they represent two individual words in the list.

For example,

Assume that words = `["practice", "makes", "perfect", "coding", "makes"]`.

Given word1 = `"makes"`, word2 = `"coding"`, return 1.
Given word1 = `"makes"`, word2 = `"makes"`, return 3.

**Note:**

You may assume word1 and word2 are both in the list.

**Solution:**
```java
public class Solution {
  public int shortestWordDistance(String[] words, String word1, String word2) {
    if (word1.equals(word2))
      return helper1(words, word1);
    else
      return helper2(words, word1, word2);
  }
    
  int helper1(String[] words, String word) {
    int p = -1, min = Integer.MAX_VALUE;
        
    for (int i = 0; i < words.length; i++) {
      if (words[i].equals(word)) {
        if (p != -1) {
          min = Math.min(min, i - p);
        }
        p = i;
      }
    }
        
    return min;
  }
    
  int helper2(String[] words, String word1, String word2) {
    int p1 = -1, p2 = -1, min = Integer.MAX_VALUE;
        
    for (int i = 0; i < words.length; i++) {
      if (words[i].equals(word1)) {
        p1 = i;
      }
            
      if (words[i].equals(word2)) {
        p2 = i;
      }
            
      if (p1 != -1 && p2 != -1) {
        min = Math.min(min, Math.abs(p1 - p2));
      }
    }
        
    return min;
  }
}
```