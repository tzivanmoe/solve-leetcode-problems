# Valid Anagram

Given two strings s and t, write a function to determine if t is an anagram of s.

For example,

s = `"anagram"`, t = `"nagaram"`, return `true`.

s = `"rat"`, t = `"car"`, return `false`.

**Note:**

You may assume the string contains only lowercase alphabets.

**Follow up:**

What if the inputs contain unicode characters? How would you adapt your solution to such case?

**Solution:**
```java
public class Solution {
  public boolean isAnagram(String s, String t) {
      if (s == null || t == null || s.length() != t.length())
        return false;

      int[] arr = new int[128];

      for (int i = 0; i < s.length(); i++) {
        arr[(int)s.charAt(i)]++;
        arr[(int)t.charAt(i)]--;
      }

      for (int i = 0; i < arr.length; i++) {
        if (arr[i] != 0) 
          return false;
      }

      return true;
  }
}
```