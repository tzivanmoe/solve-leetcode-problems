# Fraction to Recurring Decimal

Given two integers representing the numerator and denominator of a fraction, return the fraction in string format.

If the fractional part is repeating, enclose the repeating part in parentheses.

For example,

* Given numerator = 1, denominator = 2, return "0.5".
* Given numerator = 2, denominator = 1, return "2".
* Given numerator = 2, denominator = 3, return "0.(6)".

**Hint:**

1. No scary math, just apply elementary math knowledge. Still remember how to perform a long division?
2. Try a long division on 4/9, the repeating part is obvious. Now try 4/333. Do you see a pattern?
3. Be wary of edge cases! List out as many test cases as you can think of and test your code thoroughly.

**Solution:**
```java
public class Solution {
  public String fractionToDecimal(int numerator, int denominator) {
    // zero denominator
    if (denominator == 0) return "NaN";

    // zero numerator
    if (numerator == 0) return "0";

    StringBuilder res = new StringBuilder();

    Long n = new Long(numerator);
    Long d = new Long(denominator);

    // determine the sign
    if (n < 0 ^ d < 0) res.append('-');

    // remove sign of operands
    n = Math.abs(n); d = Math.abs(d);

    // append integral part
    res.append(Long.toString(n / d));

    // in case no fractional part
    if (n % d == 0) return res.toString();

    res.append('.');

    Map<Long, Integer> map = new HashMap<Long, Integer>();

    // simulate the division process
    for (Long r = n % d; r > 0; r %= d) {
      // meet a known remainder
      // so we reach the end of the repeating part
      if (map.containsKey(r)) {
        res.insert(map.get(r), "(");
        res.append(")");
        break;
      }

      // the remainder is first seen
      // remember the current position for it
      map.put(r, res.length());

      r *= 10;

      // append the quotient digit
      res.append(Long.toString(r / d));
    }

    return res.toString();
  }
}
```