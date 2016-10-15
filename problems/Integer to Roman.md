# Integer to Roman

Given an integer, convert it to a roman numeral.

Input is guaranteed to be within the range from 1 to 3999.

**Solution:**
```java
public class Solution {
  private char[][] romans = {
    {'I', 'V', 'X'},
    {'X', 'L', 'C'},
    {'C', 'D', 'M'},
    {'M', ' ', ' '}
  };

  public String intToRoman(int num) {
    StringBuilder sb = new StringBuilder();

    ArrayList<Integer> digits = new ArrayList<Integer>();

    while (num > 0) {
      digits.add(num % 10);
      num /= 10;
    }

    int size = digits.size();

    for (int i = size - 1; i >= 0; i--) {
      String roman = getRoman(i, digits.get(i));
      sb.append(roman);
    }

    return sb.toString();
  }

  private String getRoman(int level, int digit) {
    char one  = romans[level][0];
    char five = romans[level][1];
    char ten  = romans[level][2];

    StringBuilder sb = new StringBuilder();

    if (digit == 9) {
      sb.append(one).append(ten);
    }

    else if (digit >= 5) {
      sb.append(five);
      for (int i = 0; i < digit - 5; i++) {
        sb.append(one);
      }
    }

    else if (digit == 4) {
      sb.append(one).append(five);
    }

    else {
      for (int i = 0; i < digit; i++) {
        sb.append(one);
      }
    }

    return sb.toString();
  }
}
```