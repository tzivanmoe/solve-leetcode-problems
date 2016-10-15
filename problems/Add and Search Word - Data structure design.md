# Add and Search Word - Data structure design

Design a data structure that supports the following two operations:
```
void addWord(word)
bool search(word)
```
search(word) can search a literal word or a regular expression string containing only letters `a-z` or `.`. A `.` means it can represent any one letter.

For example:
```
addWord("bad")
addWord("dad")
addWord("mad")
search("pad") -> false
search("bad") -> true
search(".ad") -> true
search("b..") -> true
```
**Note:**

You may assume that all words are consist of lowercase letters `a-z`.

You should be familiar with how a Trie works. If not, please work on this problem: Implement Trie (Prefix Tree) first.

**Solution:**
```java
public class WordDictionary {
    
  Trie trie = new Trie();

  // Adds a word into the data structure.
  public void addWord(String word) {
    trie.insert(word);
  }

  // Returns if the word is in the data structure. A word could
  // contain the dot character '.' to represent any one letter.
  public boolean search(String word) {
    return trie.search(word);
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
      return dfs(root, word, 0);
    }
        
    private boolean dfs(TrieNode node, String word, int index) {
      if (node == null || index == word.length() && !node.isLeaf)
        return false;
                
      if (node.isLeaf && index == word.length())
        return true;
                
      char c = word.charAt(index);
            
      if (c == '.') {
        for (char ch = 'a'; ch <= 'z'; ch++) {
          if (dfs(node.children.get(ch), word, index + 1))
            return true;
        }
                
        return false;
      } else {
        return dfs(node.children.get(c), word, index + 1);
      }
    }
  }
}

// Your WordDictionary object will be instantiated and called as such:
// WordDictionary wordDictionary = new WordDictionary();
// wordDictionary.addWord("word");
// wordDictionary.search("pattern");
```