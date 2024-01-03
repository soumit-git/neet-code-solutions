# 125. Valid Palindrome

A phrase is a palindrome if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

Given a string s, return true if it is a palindrome, or false otherwise.

 

Example 1:

Input: s = "A man, a plan, a canal: Panama"
Output: true
Explanation: "amanaplanacanalpanama" is a palindrome.
Example 2:

Input: s = "race a car"
Output: false
Explanation: "raceacar" is not a palindrome.
Example 3:

Input: s = " "
Output: true
Explanation: s is an empty string "" after removing non-alphanumeric characters.
Since an empty string reads the same forward and backward, it is a palindrome.
 

Constraints:

- 1 <= s.length <= 2 * 105
- s consists only of printable ASCII characters.

## Solution 
### 1. Two pointer solution:
```
class Solution:
    def isPalindrome(self, s: str) -> bool:
        l = 0
        r = len(s) - 1

        while l < r:
          while l < r and not s[l].isalnum():
            l += 1
          while r > l and not s[r].isalnum():
            r -= 1
          if s[l].lower() != s[r].lower():
            return False
          l, r = l+1, r-1
        
        return True
```

### 2. built in library solution:
```
class Solution:
    def isPalindrome(self, s: str) -> bool:
      s2 = ''
      for i in s.lower():
        if i.isalnum():
          s2 += i
      return s2 == s2[::-1]
```