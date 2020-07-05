# Palindrome Partitioning
# https://leetcode.com/problems/palindrome-partitioning

# Implementation :
```java
class Solution {
    public List<List<String>> partition(String str) {
        List<List<String>> res = new ArrayList<>();
        if (str.length() == 0) return res;
        helper(res, new ArrayList<String>(), str, 0);
        return res;
    }
    
    private void helper(List<List<String>> res, List<String> current, String str, int start) {
    	// System.out.println("helper(res, current, str, " + start+")");
        if (start == str.length()) {
        	// System.out.println(" Adding : " + current);
            res.add(new ArrayList<>(current));
            return;
        }
        
        int n = str.length();
        for (int j = start; j < n; j++) {
            if (isPalindrome(str, start, j)) {
            	// System.out.println("Palindrome : " + str.substring(start, j + 1));
            	current.add(str.substring(start, j + 1));
                helper(res, current, str, j + 1);
                current.remove(current.size() - 1);
            }
        }
    }
    
    private boolean isPalindrome(String str, int start, int end) {
        while (start <= end) {
            if (str.charAt(start++) != str.charAt(end--)) 
            	return false;
        }
        return true;
    }

}
```

**Runtime Analysis :**

Time complexity: O(n*(2^n))

For a string with length n, there will be (n - 1) intervals between chars.

For every interval, we can cut it or not cut it, so there will be 2^(n - 1) ways to partition the string.

For every partition way, we need to check if it is palindrome, which is O(n).

So the time complexity is O(n*(2^n))

# References :
1. https://www.youtube.com/watch?v=A0wENqSIxK4
2. https://leetcode.com/problems/palindrome-partitioning/discuss/41963/Java:-Backtracking-solution./40308
