---
layout: post
title: <Greedy> 860. Lemonade Change [Easy]
---

## Leetcode [Greedy] 942. DI String Match[Easy]

**942. DI String Match [Easy]**

---

A permutation `perm` of `n + 1` integers of all the integers in the range `[0, n]` can be represented as a string `s` of length `n` where:

- `s[i] == 'I'` if `perm[i] < perm[i + 1]`, and
- `s[i] == 'D'` if `perm[i] > perm[i + 1]`.

Given a string `s`, reconstruct the permutation `perm` and return it. If there are multiple valid permutations perm, return **any of them**.

---

**Example 1:**

```
Input: s = "IDID"
Output: [0,4,1,3,2]

```

**Example 2:**

```
Input: s = "III"
Output: [0,1,2,3]

```

**Example 3:**

```
Input: s = "DDI"
Output: [3,2,0,1]

```

**Constraints:**

- `1 <= s.length <= 105`
- `s[i]` is either `'I'` or `'D'`.

---

- **문제 설명**

> input에는 I나 D가 들어옵니다.
- I가 들어오는 경우는 현재 index의 숫자보다 다음 숫자(index+1)의 숫자가  클 경우를 말합니다.
- D가 들어오는 경우는 현재 index의 숫자보다 다음 숫자(index+1)의 숫자가 작을 경우를 말합니다.
받아온 문자열이 만족할 수 있는 숫자 배열을 리턴해주면 됩니다.
> 

---

- **문제 풀이**
1. “I”가 들어올 경우 0부터 시작해서 +1씩 증가하면서 배열에 저장합니다.
2. “D”가 들어올 경우 s의 length부터 시작해서 -1씩 감소하면서 배열에 저장합니다.
3. S문자열에 대하여 한문자씩 꺼내와 비교하면서 숫자배열을 완성시킵니다.
4. 마지막 문자를 검사하여 “I”였다면, “I”의 조건인 다음숫자가 크도록 iVal을 저장합니다.
5. 마지막 문자를 검사하여 “D”라면, “D”의 조건인 다음숫자가 작도록 dVal을 저장합니다.

---

### Swift로 작성한 코드는 아래와 같습니다.

```swift
class Solution {
    func diStringMatch(_ s: String) -> [Int] {
        var iVal = 0
        var dVal = s.count

        var result = [Int]()
        for i in s {
            if i == "I" {
                result.append(iVal)
                iVal += 1
            } else {
                result.append(dVal)
                dVal -= 1
            }
        }
        if let last = s.last, last == "I" {
            result.append(iVal)
        } else {
            result.append(dVal)
        }
        
        return result
    }
}
```
