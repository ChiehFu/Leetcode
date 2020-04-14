---
title: Perform String Shifts
tags: String
notebook: Leetcode
---
You are given a string s containing lowercase English letters, and a matrix shift, where shift[i] = [direction, amount]:

- direction can be 0 (for left shift) or 1 (for right shift). 
- amount is the amount by which string s is to be shifted.
- A left shift by 1 means remove the first character of s and append it to the end.
- Similarly, a right shift by 1 means remove the last character of s and add it to the beginning.

Return the final string after all operations.

 
```
Example 1:

Input: s = "abc", shift = [[0,1],[1,2]]
Output: "cab"
Explanation: 
[0,1] means shift to left by 1. "abc" -> "bca"
[1,2] means shift to right by 2. "bca" -> "cab"
```
Example 2:
```
Input: s = "abcdefg", shift = [[1,1],[1,1],[0,2],[1,3]]
Output: "efgabcd"
Explanation:  
[1,1] means shift to right by 1. "abcdefg" -> "gabcdef"
[1,1] means shift to right by 1. "gabcdef" -> "fgabcde"
[0,2] means shift to left by 2. "fgabcde" -> "abcdefg"
[1,3] means shift to right by 3. "abcdefg" -> "efgabcd"
```

Constraints:

- 1 <= s.length <= 100
- s only contains lower case English letters.
- 1 <= shift.length <= 100
- shift[i].length == 2
- 0 <= shift[i][0] <= 1
- 0 <= shift[i][1] <= 100
----------
Thoughts:
1. Calculate how many left/right shifts are requested and represent that amount as `totalLeftShift`, of which the positive value means the amount of left shift and the negative value means the amount of right shift.
2. Mod `totalLeftShift` by `s.length()` to make it positive, which will be the final amount of left shift required to be performed.
3. Splice the string with the right index to make that shift completed.
   
```Java
// Time: O(N)
// Space: O(1)

class Solution {
    public String stringShift(String s, int[][] shift) {
        int totalLeftShift = 0;
        for (int i = 0; i < shift.length; ++i) {
            int amount = (shift[i][0] == 0? 1 : -1) * shift[i][1];
            totalLeftShift += amount;
        }

        totalLeftShift = Math.floorMod(totalLeftShift, s.length());

        if (totalLeftShift < 0) {
            totalLeftShift += s.length();
        }
        s = s.substring(totalLeftShift) + s.substring(0, totalLeftShift);
        return s;
    }
}
```