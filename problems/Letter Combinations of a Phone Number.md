# Letter Combinations of a Phone Number

Given a digit string, return all possible letter combinations that the number could represent.

A mapping of digit to letters (just like on the telephone buttons) is given below.

![](200px-Telephone-keypad2.svg.png)

```
Input:Digit string "23"
Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
```

**Note:**

Although the above answer is in lexicographical order, your answer could be in any order you want.

**Solution:**
```java
public class Solution {
  public List<String> letterCombinations(String digits) {
    String[] keyboard = {" ", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};
		
	List<String> res = new ArrayList<String>();
		
	helper(digits, keyboard, 0, "", res);
		
	return res;
  }
    
  private void helper(String digits, String[] keyboard, int index, String sol, List<String> res) {
    if (sol.length() == digits.length()) {
        res.add(sol);
        return;
    }
        
    int idx = (int)(digits.charAt(index) - '0');
    String key = keyboard[idx];
        
    for (int i = 0; i < key.length(); i++) {
      helper(digits, keyboard, index + 1, sol + key.charAt(i), res);
    }
  }
}
```