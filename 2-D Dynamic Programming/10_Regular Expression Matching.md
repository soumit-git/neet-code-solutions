# 10. Regular Expression Matching
Given an input string s and a pattern p, implement regular expression matching with support for '.' and '*' where:

'.' Matches any single character.​​​​
'*' Matches zero or more of the preceding element.
The matching should cover the entire input string (not partial).

 

Example 1:

Input: s = "aa", p = "a"
Output: false
Explanation: "a" does not match the entire string "aa".
Example 2:

Input: s = "aa", p = "a*"
Output: true
Explanation: '*' means zero or more of the preceding element, 'a'. Therefore, by repeating 'a' once, it becomes "aa".
Example 3:

Input: s = "ab", p = ".*"
Output: true
Explanation: ".*" means "zero or more (*) of any character (.)".
 

Constraints:

1 <= s.length <= 20
1 <= p.length <= 20
s contains only lowercase English letters.
p contains only lowercase English letters, '.', and '*'.
It is guaranteed for each appearance of the character '*', there will be a previous valid character to match.

## Solution
```
class Solution:
    def isMatch(self, s: str, p: str) -> bool:
        cache = {}
        def dfs(i, j):
          if (i, j) in cache:
            return cache[(i, j)]
          if i >= len(s) and j >= len(p):
            return True
          if j >= len(p):
            return False
          
          match = (i < len(s)) and (s[i] == p[j] or p[j] == '.')
          if (j + 1) < len(p) and p[j + 1] == '*':
            cache[(i, j)] = (dfs(i, j + 2) or (match and dfs(i + 1, j)))
            return cache[(i, j)]
          
          if match:
            cache[(i, j)] = dfs(i + 1, j + 1)
            return cache[(i, j)]
          
          cache[(i, j)] = False
          return False
        
        return dfs(0, 0)
```