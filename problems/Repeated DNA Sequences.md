# Repeated DNA Sequences

All DNA is composed of a series of nucleotides abbreviated as A, C, G, and T, for example: "ACGAATTCCG". When studying DNA, it is sometimes useful to identify repeated sequences within the DNA.

Write a function to find all the 10-letter-long sequences (substrings) that occur more than once in a DNA molecule.

For example,
```
Given s = "AAAAACCCCCAAAAACCCCCCAAAAAGGGTTT",

Return:
["AAAAACCCCC", "CCCCCAAAAA"].
```

**Solution:**
```java
public class Solution {
  public List<String> findRepeatedDnaSequences(String s) {
    int len = s.length();

    if (len < 10) {
      return new LinkedList<String>();
    }

    int a = 0;
    int m = 1;

    for (int i = 0; i < 10; i++) {
      a = a * 4 + getCode(s.charAt(i));
      m *= 4;
    }

    HashSet<Integer> set = new HashSet<Integer>();
    HashSet<Integer> r = new HashSet<Integer>();
    LinkedList<String> result = new LinkedList<String>();

    set.add(a);

    int p = 10;

    while (p < len) {
      a = (a * 4 + getCode(s.charAt(p))) % m;

      if (set.contains(a) && !r.contains(a)) {
        result.add(s.substring(p - 9, p + 1));
        r.add(a);
      }
      else {
        set.add(a);
      }

      p++;
    }

    return result;
  }

  private int getCode(char c) {
    if (c == 'C') return 1;
    if (c == 'G') return 2;
    if (c == 'T') return 3;
    return 0;
  }
}
```