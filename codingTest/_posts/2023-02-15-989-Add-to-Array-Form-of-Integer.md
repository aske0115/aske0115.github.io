# Leetcode [Array] 989. Add to Array-Form of Integer [Easy]

생성일: February 15, 2023 1:24 PM

**989. Add to Array-Form of Integer [Easy]**

The **array-form** of an integer `num` is an array representing its digits in left to right order.

- For example, for `num = 1321`, the array form is `[1,3,2,1]`.

Given `num`, the **array-form** of an integer, and an integer `k`, return *the **array-form** of the integer* `num + k`.

**Example 1:**

```
Input: num = [1,2,0,0], k = 34
Output: [1,2,3,4]
Explanation: 1200 + 34 = 1234

```

**Example 2:**

```
Input: num = [2,7,4], k = 181
Output: [4,5,5]
Explanation: 274 + 181 = 455

```

**Example 3:**

```
Input: num = [2,1,5], k = 806
Output: [1,0,2,1]
Explanation: 215 + 806 = 1021

```

**Constraints:**

- `1 <= num.length <= 104`
- `0 <= num[i] <= 9`
- `num` does not contain any leading zeros except for the zero itself.
- `1 <= k <= 104`

---

- **문제 설명**

> 입력된 숫자 배열 num과 숫자 k를 더한 값을 숫자배열로 리턴해야 하는 문제입니다.
> 

---

- **문제 풀이**
1. 최초 생각했던 풀이는, nums를 String으로 변환 후, 다시 Int로 변환해서 k와 더해준 후, 다시 [Int]로 map 해서 리턴해주는 방식이었습니다.
    1. 그러나 nums의 자리수가 Int의 범위를 초과하는 이슈가 있어 풀이를 변경하였습니다.
    2. 그래서 nums를 Int로 변경하지 않고, 존재하는 num의 마지막 인덱스부터 sum하면서 값을 교체하는 방식으로 생각을 전환하였습니다.
2. 숫자로 입력된 k를 숫자배열로 변환하고, 각각 마지막 index부터 앞자리로 옮겨가면서 sum을 하고,upper 변수를 추가하여, 더한 값이 반올림을 해야하는지 판단해서 다음 로직을 처리합니다.
    1. k가 num보다 클 경우는 result 배열 맨 앞에 계산결과를 새로 이어붙혀주고,
    2. k를 다 돌았지만 num이 아직 남아있을 경우, 반올림이 끝날 때 까지, 값을 올려줍니다.
    3. 모든 로직을 종료하고나서 upper가 true일 경우,,(999+1의 경우 다 계산한 후 맨 앞에 올림수(1)이 필요하므로 그에 대한 처리를 해주는 방식으로 마무리하였습니다.

---

### Swift로 작성한 코드는 아래와 같습니다.

```swift
class Solution {
    func addToArrayForm(_ num: [Int], _ k: Int) -> [Int] {
        var result = num
        var kNum = String(k).compactMap { $0.wholeNumberValue }.reversed()
        var numIndex = num.count - 1
        var upper = false
        
        for i in kNum {
            let sum = (numIndex > -1 ? result[numIndex] : 0) + i + (upper ? 1 : 0)
            upper = sum > 9
            let value = upper ? sum % 10 : sum
            if numIndex > -1 {
                result[numIndex] = value
            } else {
                result.insert(value, at: result.startIndex)
            }
            numIndex -= 1
        }
        
        while upper && numIndex >= 0 {
            if result[numIndex] > 8 {
                result[numIndex] = 0
            } else {
                result[numIndex] += 1
                upper = false
            }
            numIndex -= 1
        }
        
        if upper {
            result.insert(1, at: result.startIndex)
        }
        
        return result
    }
}
```

---
<script src="https://utteranc.es/client.js"
        repo="aske0115/blog-comments"
        issue-term="pathname"
        label="utterences"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>
