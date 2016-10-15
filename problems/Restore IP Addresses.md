# Restore IP Addresses

Given a string containing only digits, restore it by returning all possible valid IP address combinations.

For example:

Given `"25525511135"`,

return `["255.255.11.135", "255.255.111.35"]`. (Order does not matter)

**Solution:**
```java
public class Solution {
  public List<String> restoreIpAddresses(String s) {
    List<String> res = new ArrayList<String>();
    helper(s, 0, 0, "", res);
    return res;
  }
    
  void helper(String s, int index, int segment, String sol, List<String> res) {
    if (segment == 4 && index == s.length()) {
      res.add(sol);
      return;
    }
        
    // too many characters left
    if (s.length() > index + (4 - segment) * 3) {
      return;
    }
        
    // not enough characters left
    if (s.length() < index + (4 - segment)) {
      return;
    }
        
    for (int i = index; i < index + 3 && i < s.length(); i++) {
      String str = s.substring(index, i + 1);
      int num = Integer.parseInt(str);
            
      if ((s.charAt(index) == '0' && i > index) || (num > 255)) {
        return;
      }
            
      helper(s, i + 1, segment + 1, sol + str + (segment == 3 ? "" : "."), res);
    }
  }
}
```