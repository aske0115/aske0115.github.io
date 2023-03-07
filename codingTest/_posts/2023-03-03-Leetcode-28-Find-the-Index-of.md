# Leetcode [String] 28. Find the Index of the First Occurrence in a String [Medium]

**28. Find the Index of the First Occurrence in a String**

---

Given two strings `needle` and `haystack`, return the index of the first occurrence of `needle` in `haystack`, or `-1` if `needle` is not part of `haystack`.

**Example 1:**

```
Input: haystack = "sadbutsad", needle = "sad"
Output: 0
Explanation: "sad" occurs at index 0 and 6.
The first occurrence is at index 0, so we return 0.

```

**Example 2:**

```
Input: haystack = "leetcode", needle = "leeto"
Output: -1
Explanation: "leeto" did not occur in "leetcode", so we return -1.

```

**Constraints:**

- `1 <= haystack.length, needle.length <= 104`
- `haystack` and `needle` consist of only lowercase English characters.

---

- **문제 설명**

> haystack에서 needle이 나타나는 인덱스를 반환하거나, needle이 haystack에 포함되지 않으면(일부문자열이 아니면) -1을 리턴하는 문제이다
> 

---

- **문제 풀이 (1)**

> 이전에 풀어보았던 문제이지만, 다른 방식으로 다시 풀어보았다.
이전 문제코드는 아래와 같으며 풀이는 다음과 같다.
> 
- 두개의 문자열이 같으면 0번 인덱스를 반환한다
- needle이 haystack보다 크다면,  needle이 haystack의 일부가 될 수 없으므로 -1을 리턴한다.
- haystack을 stringArray로 변환하여, needle만큼의 range를 잘라서 needle과 같은지 비교하는 반복문을 수행하여 해당 인덱스를 반환한다.

### 이전 코드는 아래와 같습니다.

```swift
class Solution {
    func strStr(_ haystack: String, _ needle: String) -> Int {
        
        if haystack == needle {
            return 0
        }
        
        if haystack.count < needle.count {
            return -1
        }
        
        let needleCount = needle.count
        let stringArray = haystack.map { String($0) }
        
        for i in 0...stringArray.count - needleCount {
            let string = stringArray[i..<i+needleCount].joined(separator:"")
            if needle == string {
                return i
            }
        }
        return -1
    }
}
```

---

위의 풀이는 매우 간단하지만 성능상 좋은 성능을 보여주지 않았습니다.

![Submit을 하고난 후 나타난 chart](/assets/img/blog/leetcode28/originSolve.png)

Submit을 하고난 후 나타난 chart

- **문제 풀이 (2)**

> two pointer index를 가지고 풀어보았다.
> 
- needle이 haystack보다 크거나, needle의 시작문자가 haystack에 없을 경우 -1을 리턴한다.
- needle의 첫 문자가 시작되는 haystack의 index부터 시작하여 한칸씩 옮겨가며 문자가 같은지 확인한다.
- 문자가 다를경우, needle의 첫 문자가 시작되는 다음의 위치를 찾아서 다시 반복한다.
    - 더이상 needle의 첫 문자와 같은 문자가 없고, 두개의 문자가 다를경우 -1을 리턴한다.
- while문이 종료되었지만 needle의 index가 아직 끝까지 도달하지 못하였다면. needle의 일부만 포함되었다고 판단이 되는것이므로 -1을 리턴하고, 그게 아니라면 일치하는 index를 리턴해준다.

### 다른 방식으로 풀어본 코드는 아래와 같습니다.

```swift
class Solution {
    func strStr(_ haystack: String, _ needle: String) -> Int {
        guard haystack.count >= needle.count, var firstIndex = haystack.firstIndex(of:needle.first!) else { return -1 }
        var needleIndex = needle.startIndex
        var haystackStartIndex = firstIndex
        
        while needleIndex < needle.endIndex, haystackStartIndex < haystack.endIndex {
            if haystack[haystackStartIndex] == needle[needleIndex] {
                haystackStartIndex = haystack.index(haystackStartIndex, offsetBy: 1)
                needleIndex = needle.index(needleIndex, offsetBy: 1)
            } else {
                if let nextIndex = haystack[haystack.index(firstIndex, offsetBy: 1)..<haystack.endIndex].firstIndex(of: needle.first!) {
                    haystackStartIndex = nextIndex
                    needleIndex = needle.startIndex
                    firstIndex = nextIndex
                    continue
                } else {
                    return -1
                }
            }
        }
        return needleIndex < needle.endIndex ? -1 : haystack.distance(from: haystack.startIndex, to: firstIndex)
    }
}
```

---

해당 풀이로 변경한 후 제출해 보았으며, 성능은 다음과 같이 개선되었습니다.

![풀이를 변경하여 Submit한 후의 chart](/assets/img/blog/leetcode28/modifySolve.png)

풀이를 변경하여 Submit한 후의 chart

