# Roman to Integer

Given a roman numeral, convert it to an integer.

Input is guaranteed to be within the range from 1 to 3999.

**Solution:**
```java
public class Solution {
  public int romanToInt(String s) {
    // Roman to Int map
    Map<Character, Integer> map = new HashMap<>();
    map.put('I', 1);
    map.put('V', 5);
    map.put('X', 10);
    map.put('L', 50);
    map.put('C', 100);
    map.put('D', 500);
    map.put('M', 1000);

    int n = s.length();
    int i = n - 1;
    int sum = map.get(s.charAt(i--));

    while (i >= 0) {
      int curr = map.get(s.charAt(i));
      int next = map.get(s.charAt(i + 1));

      if (curr >= next) {
        sum += curr;
      } else {
        sum -= curr;
      }

      i--;
    }

    return sum;
  }
}
```