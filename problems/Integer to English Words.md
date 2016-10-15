# Integer to English Words

Convert a non-negative integer to its english words representation. Given input is guaranteed to be less than 231 - 1.

For example,
```
123 -> "One Hundred Twenty Three"
12345 -> "Twelve Thousand Three Hundred Forty Five"
1234567 -> "One Million Two Hundred Thirty Four Thousand Five Hundred Sixty Seven"
```

**Hint:**

* Did you see a pattern in dividing the number into chunk of words? For example, 123 and 123000.
* Group the number by thousands (3 digits). You can write a helper function that takes a number less than 1000 and convert just that chunk to words.
* There are many edge cases. What are some good test cases? Does your code work with input such as 0? Or 1000010? (middle chunk is zero and should not be printed out)

**Solution:**
```java
public class Solution {
  String[] bigs = "Hundred Thousand Million Billion".split(" ");
  String[] tens = "Twenty Thirty Forty Fifty Sixty Seventy Eighty Ninety".split(" ");
  String[] lows = "Zero One Two Three Four Five Six Seven Eight Nine Ten Eleven Twelve Thirteen Fourteen Fifteen Sixteen Seventeen Eighteen Nineteen".split(" ");

  public String numberToWords(int n) {
    if (n < 20) 
      return lows[n];

    if (n < 100)
      return tens[n / 10 - 2] + helper(n % 10);

    if (n < 1000) 
      return lows[n / 100] + " " + bigs[0] + helper(n % 100);

    int m = 1000;

    for (int i = 1; i < bigs.length; i++, m *= 1000)
      if (n / 1000 < m)
        return numberToWords(n / m) + " " + bigs[i] + helper(n % m);

    return numberToWords(n / m) + " " + bigs[bigs.length - 1] + helper(n % m);
  }

  public String helper(int n) {
    return n == 0 ? "" : " " + numberToWords(n);
  }
}
```