# Implement Trie

Implement a trie with `insert`, `search`, and `startsWith` methods.

**Note:**

You may assume that all inputs are consist of lowercase letters `a-z`.

**Solution:**
```java
class TrieNode {
  char c;
  boolean isLeaf;
  Map<Character, TrieNode> children = new HashMap<>();

  public TrieNode() {}
  public TrieNode(char c) {
    this.c = c;
  }
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

      if (!children.containsKey(c)) {
        children.put(c, new TrieNode(c));
      }

      if (i == word.length() - 1) {
        children.get(c).isLeaf = true;
      }

      children = children.get(c).children;
    }
  }

  // Returns if the word is in the trie.
  public boolean search(String word) {
    TrieNode node = getLastTrieNode(word);
    return node != null && node.isLeaf;
  }

  // Returns if there is any word in the trie
  // that starts with the given prefix.
  public boolean startsWith(String prefix) {
    TrieNode node = getLastTrieNode(prefix);
    return node != null;
  }

  private TrieNode getLastTrieNode(String word) {
    Map<Character, TrieNode> children = root.children;

    for (int i = 0; i < word.length(); i++) {
      char c = word.charAt(i);

      if (!children.containsKey(c)) {
        break;
      }

      if (i == word.length() - 1)
        return children.get(c);

      children = children.get(c).children;
    }

    return null;
  }
}

// Your Trie object will be instantiated and called as such:
// Trie trie = new Trie();
// trie.insert("somestring");
// trie.search("key");
```