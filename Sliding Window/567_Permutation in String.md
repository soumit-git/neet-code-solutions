# 567. Permutation in String
Given two strings s1 and s2, return true if s2 contains a permutation of s1, or false otherwise.

In other words, return true if one of s1's permutations is the substring of s2.

 

Example 1:

Input: s1 = "ab", s2 = "eidbaooo"
Output: true
Explanation: s2 contains one permutation of s1 ("ba").
Example 2:

Input: s1 = "ab", s2 = "eidboaoo"
Output: false
 

Constraints:

1 <= s1.length, s2.length <= 104
s1 and s2 consist of lowercase English letters.
## Solution

```
class Solution:
    def checkInclusion(self, s1: str, s2: str) -> bool:
      l1, l2 = len(s1), len(s2)
      if l1>l2: return False ## edge cases
      c1, c2 = Counter(s1), Counter(s2[:l1])
      for i in range(l2-l1):
          if c1==c2: return True
          char1, char2 = s2[i], s2[i+l1]
          c2[char1] -= 1 ## update counter c2
          if c2[char1]==0: 
              del c2[char1]
          c2[char2] += 1
      return c1==c2
```