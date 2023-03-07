---
layout: post
title: <Greedy> 680. Valid Palindrome II [Easy]
---


## Leetcode [Greedy] 680. Valid Palindrome II [Easy]
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
 
**문제설명** 
> 해당 문제는 주어진 문자열이 원래부터  palindrome이거나, 아닐경우, 최대 1개의 문자를 제거했을 때 palindrome이 되는지 확인하는 문제입니다.   
> > palindrome : asdsa, aba, aabbcccbbaa eye 와 같이, 왼쪽에서 오른쪽으로 읽으나, 오른쪽에서 왼쪽으로 읽으나 같은 문자열이 되는 것을 말합니다.   

    
    
 **해결방법**   
> 여기서 저는 two pointer를 사용하여,  first는 처음에서 + 1씩 증가하여 오른쪽으로 이동하고,    
> last는 맨 마지막에서 -1 씩 감소하여 왼쪽으로 이동하면서,   
> 앞뒤가 같은지 확인하는 isPalindrom 함수를 별도로 추가하여, 넘겨받은 문자열이 palidrome을 만족하는지 판단하도록 하였습니다.   
> 그 후, 원래의 문자열도 동일하게 first와 last를 이용하여 앞뒤가 같은지를 확인하는 로직을 수행하도록 하였으며,   
> * 같지 않을 경우   
 > > 현재 위치한 문자열 다음부터 마지막까지의 slice된 문자열을 넘겨주어 palindrome을 확인하거나, 
 > > 현재 위치한 문자열부터 마지막 바로 전까지의 slice된 문자열을 넘겨주어 palindrome을 확인하여, 둘중 하나라도 true이면 true가 리턴됩니다.
> * 같을 경우
 > > first와 last의 인덱스를 각각 오른쪽, 왼쪽으로 옮겨서 다시 서로의 문자가 같은지 확인합니다.
 
```
 해당 이유는 최대 1개의 문자만 삭제할 수 있다는 조건때문에, 현재 first인덱스 다음글자부터 남은 문자열을 확인하거나,    
 현재 first인덱스부터 last인덱스 바로 앞까지 범위를 지정하여, 맨 마지막 글자를 제거한 남은 문자열을 확인하도록 하였습니다.   
 ```
 
 
```
 최초 답안 제출시에는, String을 Array로 변환하지 않고, string의 index 함수를 사용하여    
 문자열을 쪼개거나, 해당 first의 문자가 무엇인지, last의 문자가 무엇인지 늘 index를 계산해서 하는 방식으로 제출하였더니    
 시간초과가 나오는 것을 보고 Array로 변환해서 index에 바로 접근 하도록 불필요한 연산을 제거하고 제출에 성공하였습니다.   
 ```
 
---   

### swift 코드로 나타내면 아래와 같습니다.

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
    }*
}
~~~
