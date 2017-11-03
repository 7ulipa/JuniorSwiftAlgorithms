[https://leetcode.com/problems/longest-substring-without-repeating-characters/description/](https://leetcode.com/problems/longest-substring-without-repeating-characters/description/)


```
Given a string, find the length of the longest substring without repeating characters.

Examples:

Given "abcabcbb", the answer is "abc", which the length is 3.

Given "bbbbb", the answer is "b", with the length of 1.

Given "pwwkew", the answer is "wke", with the length of 3. Note that the answer must be a substring, "pwke" is a subsequence and not a substring.
```


```
class Solution {
    func lengthOfLongestSubstring(_ s: String) -> Int {
        var l = 0, r = 0
        let chars = s.utf8CString.dropLast()
        var set: Set<CChar> = []
        var result = 0
        while r < chars.count {
            let char = chars[r]
            while set.contains(char) {
                set.remove(chars[l])
                l += 1
            }
            set.insert(char)
            result = max(result, set.count)
            r += 1
        }
        return result
    }
}
```
