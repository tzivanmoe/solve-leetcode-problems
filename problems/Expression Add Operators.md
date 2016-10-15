# Expression Add Operators

Given a string that contains only digits `0-9` and a target value, return all possibilities to add binary operators (not unary) `+`, `-`, or `*` between the digits so they evaluate to the target value.

Examples: 
```
"123", 6 -> ["1+2+3", "1*2*3"] 
"232", 8 -> ["2*3+2", "2+3*2"]
"105", 5 -> ["1*0+5","10-5"]
"00", 0 -> ["0+0", "0-0", "0*0"]
"3456237490", 9191 -> []
```

**Solution:**
```java
public class Solution {
  public List<String> addOperators(String num, int target) {
    List<String> res = new ArrayList<>();

    if (num == null || num.length() == 0) 
      return res;

    helper(num, target, 0, 0, 0, "", res);

    return res;
  }

  public void helper(String num, int target, int index, long total, long last, String sol, List<String> res){
    if (index == num.length()) {
      if (target == total)
        res.add(sol);

      return;
    }

    for (int i = index; i < num.length(); i++) {
      // for example, input is "105", we don't need answer like "1*05"
      if (i > index && num.charAt(index) == '0') 
        break;

      long curr = Long.parseLong(num.substring(index, i + 1));

      if (index == 0) {
        // 第一个数
        helper(num, target, i + 1, curr, curr, sol + curr, res);
      } else {
        // 不是第一个数, 我们可以添加运算符了
        helper(num, target, i + 1, total + curr,  curr, sol + "+" + curr, res);
        helper(num, target, i + 1, total - curr, -curr, sol + "-" + curr, res);
        helper(num, target, i + 1, total - last + last * curr, last * curr, sol + "*" + curr, res);
      }
    }
  }
}
```