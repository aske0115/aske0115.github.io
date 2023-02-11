---
layout: post
title: <Greedy> 680. Valid Palindrome II
---


## Leetcode [Greedy] 680. Valid Palindrome II
---
Given a string s, return true if the s can be palindrome after deleting at most one character from it.

 
```
Example 1:   

Input: s = "aba"
Output: true  
```
```
Example 2:   

Input: s = "abca"
Output: true
Explanation: You could delete the character 'c'.
 ```
```
Example 3:   

Input: s = "abc"
Output: false
 ```
```
Constraints:

- 1 <= s.length <= 105.  
- s consists of lowercase English letters.    
```
---

~~~swift
class Solution {
    func validPalindrome(_ s: String) -> Bool {
        func isPalindrom(_ s: [String]) -> Bool {
            var first = 0
            var last = s.count - 1
            while first < last {
                if s[first] != s[last] {
                    return false
                } else {
                    first += 1
                    last -= 1
                }
            }
            return true
        }
        
        let stringArray = s.map { String($0) }
        var first = 0
        var last = stringArray.count - 1
        
        while first < last {
            if stringArray[first] != stringArray[last] {
                return isPalindrom(Array(stringArray[first + 1...last])) 
                       || isPalindrom(Array(stringArray[first...last - 1]))
            } else {
                first += 1
                last -= 1
            }
        }
        
        return true
    }
}
~~~
<script src="https://utteranc.es/client.js"
        repo="aske0115/blog-comments"
        issue-term="pathname"
        label="utterences"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>
