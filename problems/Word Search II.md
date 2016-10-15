# Word Search II

Given a 2D board and a list of words from the dictionary, find all words in the board.

Each word must be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once in a word.

For example,
Given **words** = `["oath","pea","eat","rain"]` and **board** =
```
[
  ['o','a','a','n'],
  ['e','t','a','e'],
  ['i','h','k','r'],
  ['i','f','l','v']
]
```
Return `["eat","oath"]`.

**Note:**

You may assume that all inputs are consist of lowercase letters `a-z`.

**Hint:**

You would need to optimize your backtracking to pass the larger test. Could you stop backtracking earlier?

If the current candidate does not exist in all words' prefix, you could stop backtracking immediately. What kind of data structure could answer such query efficiently? Does a hash table work? Why or why not? How about a Trie? If you would like to learn how to implement a basic trie, please work on this problem: Implement Trie (Prefix Tree) first.

**Solution:**
```java
public class Solution {
  int[] dx = {-1, 1, 0, 0};
  int[] dy = {0, 0, -1, 1};
    
  public List<String> findWords(char[][] board, String[] words) {
    List<String> res = new ArrayList<String>();
        
    int n = board.length;
    int m = board[0].length;
        
    boolean[][] used = new boolean[n][m];
        
    // use a hashset to avoid duplicates
    Set<String> set = new HashSet<String>();
        
    // use a trie tree to avoid unnecessary search
    Trie trie = new Trie();
    for (String word : words)
      trie.insert(word);
        
    // perform dfs from each position
    for (int i = 0; i < n; i++)
      for (int j = 0; j < m; j++)
        search(board, n, m, i, j, "", used, trie, set, res);
        
    return res;
  }
    
  void search(char[][] board, int n, int m, int i, int j, String word, boolean[][] used, Trie trie, Set<String> set, List<String> res) {
    if (i < 0 || i >= n || j < 0 || j >= m || used[i][j]) 
      return;
            
    word += board[i][j];
        
    // not the word we are looking for
    if (!trie.startsWith(word)) 
      return;
        
    if (!set.contains(word) && trie.search(word)) {
      // found the word
      set.add(word);
      res.add(word);
    }
        
    used[i][j] = true;
        
    for (int d = 0; d < 4; d++)
      // continue dfs
      search(board, n, m, i + dx[d], j + dy[d], word, used, trie, set, res);
        
    // backtracking
    used[i][j] = false;
  }
    
  class TrieNode {
    // Initialize your data structure here.
    char c;
    boolean isLeaf;
    Map<Character, TrieNode> children = new HashMap<Character, TrieNode>();
        
    public TrieNode() {}
    public TrieNode(char c) { this.c = c; }
  }

  public class Trie {
    private TrieNode root;
    
    public Trie() {
      root = new TrieNode();
    }
    
    // Inserts a word into the trie.
    public void insert(String word) {
      Map<Character, TrieNode> children = root.children;
            
      for (int i = 0; i < word.length(); i++) {
        char c = word.charAt(i);
                
        if (!children.containsKey(c))
          children.put(c, new TrieNode(c));
                
        TrieNode t = children.get(c);
                
        if (i == word.length() - 1) 
          t.isLeaf = true;
                
        children = t.children;
      }
    }
    
    // Returns if the word is in the trie.
    public boolean search(String word) {
      TrieNode t = searchLastNode(word);
            
      return t != null && t.isLeaf;
    }
    
    // Returns if there is any word in the trie
    // that starts with the given prefix.
    public boolean startsWith(String prefix) {
      return searchLastNode(prefix) != null;
    }
        
    // Returns the last TrieNode of word
    private TrieNode searchLastNode(String word) {
      Map<Character, TrieNode> children = root.children;
            
      for (int i = 0; i < word.length(); i++) {
        char c = word.charAt(i);
                
        if (!children.containsKey(c)) 
          break;
                    
        TrieNode t = children.get(c);
                
        if (i == word.length() - 1) 
          return t;
                
        children = t.children;
      }
            
      return null;
    }
  }
}
```