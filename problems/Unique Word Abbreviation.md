# Unique Word Abbreviation

An abbreviation of a word follows the form <first letter><number><last letter>. Below are some examples of word abbreviations:

```
a) it                      --> it    (no abbreviation)

     1
b) d|o|g                   --> d1g

              1    1  1
     1---5----0----5--8
c) i|nternationalizatio|n  --> i18n

              1
     1---5----0
d) l|ocalizatio|n          --> l10n
```

Assume you have a dictionary and given a word, find whether its abbreviation is unique in the dictionary. A word's abbreviation is unique if no other word from the dictionary has the same abbreviation.

**Example:**

```
Given dictionary = [ "deer", "door", "cake", "card" ]

isUnique("dear") -> false
isUnique("cart") -> true
isUnique("cane") -> false
isUnique("make") -> true
```

**Solution:**
```java
public class ValidWordAbbr {
  Map<String, Set<String>> map = new HashMap<>();

  public ValidWordAbbr(String[] dictionary) {
    // build the hashmap
    // the key is the abbreviation
    // the value is a hash set of the words that have the same abbreviation
    for (int i = 0; i < dictionary.length; i++) {
      String a = abbr(dictionary[i]);
      Set<String> set = map.containsKey(a) ? map.get(a) : new HashSet<>();
      set.add(dictionary[i]);
      map.put(a, set);
    }
  }

  public boolean isUnique(String word) {
    String a = abbr(word);
    // it's unique when the abbreviation does not exist in the map or
    // it's the only word in the set
    return !map.containsKey(a) || (map.get(a).contains(word) && map.get(a).size() == 1);
  }

  String abbr(String s) {
    if (s.length() < 3) 
      return s;

    return s.substring(0, 1) + String.valueOf(s.length() - 2) + s.substring(s.length() - 1);
  }
}


// Your ValidWordAbbr object will be instantiated and called as such:
// ValidWordAbbr vwa = new ValidWordAbbr(dictionary);
// vwa.isUnique("Word");
// vwa.isUnique("anotherWord");
```