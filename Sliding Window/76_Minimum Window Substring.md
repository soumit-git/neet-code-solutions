# 76. Minimum Window Substring
Given two strings s and t of lengths m and n respectively, return the minimum window 
substring
 of s such that every character in t (including duplicates) is included in the window. If there is no such substring, return the empty string "".

The testcases will be generated such that the answer is unique.

 

Example 1:

Input: s = "ADOBECODEBANC", t = "ABC"
Output: "BANC"
Explanation: The minimum window substring "BANC" includes 'A', 'B', and 'C' from string t.
Example 2:

Input: s = "a", t = "a"
Output: "a"
Explanation: The entire string s is the minimum window.
Example 3:

Input: s = "a", t = "aa"
Output: ""
Explanation: Both 'a's from t must be included in the window.
Since the largest window of s only has one 'a', return empty string.
 

Constraints:

m == s.length
n == t.length
1 <= m, n <= 105
s and t consist of uppercase and lowercase English letters.

## Solution
```
class Solution:
    def minWindow(self, s: str, t: str) -> str:
        td = defaultdict(int)
        sd = defaultdict(int)

        for i in t:
            td[i] += 1

        l = 0
        ans = ""

        la = float("inf")

        def checker():
            for key in td:
                if sd[key] < td[key]:
                    return False
            return True

        for r in range(len(s)):
            if s[r] in td:
                sd[s[r]] += 1


            while checker():
                na = s[l:r+1]
                if len(na) < la:
                    ans = na
                    la = len(ans)

                if s[l] in sd:
                    sd[s[l]] -= 1


                l += 1

        return ans
```