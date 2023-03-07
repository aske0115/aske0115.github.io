# Leetcode [Greedy] 2160. Minimum Sum of Four Digit Number After Splitting Digits [Easy]
---

**2160. Minimum Sum of Four Digit Number After Splitting Digits [Easy]**

---

You are given a **positive** integer `num` consisting of exactly four digits. Split `num` into two new integers `new1` and `new2` by using the **digits** found in `num`. **Leading zeros** are allowed in `new1` and `new2`, and **all** the digits found in `num` must be used.

- For example, given `num = 2932`, you have the following digits: two `2`'s, one `9` and one `3`. Some of the possible pairs `[new1, new2]` are `[22, 93]`, `[23, 92]`, `[223, 9]` and `[2, 329]`.

Return *the **minimum** possible sum of* `new1` *and* `new2`.

**Example 1:**

```
Input: num = 2932
Output: 52
Explanation: Some possible pairs [new1, new2] are [29, 23], [223, 9], etc.
The minimum sum can be obtained by the pair [29, 23]: 29 + 23 = 52.

```

**Example 2:**

```
Input: num = 4009
Output: 13
Explanation: Some possible pairs [new1, new2] are [0, 49], [490, 0], etc.
The minimum sum can be obtained by the pair [4, 9]: 4 + 9 = 13.

```

**Constraints:**

- `1000 <= num <= 9999`

---

- **문제 설명**

> 주어진 정수로 다양한 2개의 숫자를 조압하여, 조합된 수를 합한 값중에 가장 작은 값을 리턴하는 문제
> 

---

- **문제 풀이**

> 먼저 입력받은 num을 배열로 만듭니다.
그리고 0이 아닌 정수만 걸러냅니다.
- 0이 아닌 정수만 걸러내는 이유는 10은 1로, 04는 4로 처리하기 위해 적용하였습니다.
걸러내진 숫자배열의 count에 따라 숫자조합을 각각 처리합니다.
> 
- 걸러내진 숫자배열의 count가 1개일 경우 (ex 1000)
    - num배열의 처음을 리턴합니다. (1)
- 걸러내진 숫자배열의 count가 2개일 경우 (ex 4009)
    - 0이 걸러내진 배열은 4,9만 남음
    - 4+9의 값을 리턴합니다.
- 걸러내진 숫자배열의 count가 3개일 경우 (ex 1098)
    - 0이 걸러내진 배열은 1,8,9만 남음
    - 1 + 89보다 18+9가 무조건 작으므로 18 + 9를 리턴합니다.
- 걸러내진 숫자배열이 count가 4개일 경우 (2932)
    - 정렬된 배열은 [2,2,3,9]가 됩니다.
    - 10의 자리가 가장 작은숫자가 오는것이 가장 작은 수가 되므로 배열의 1번쨰와 2번째를 10의 자리수로 하고 나머지를 각각 1의 자리수로 정하여 두개의 합을 리턴합니다. (23 + 29)

---

### Swift로 작성한 코드는 아래와 같습니다.

```swift
class Solution {
    func minimumSum(_ num: Int) -> Int {
        var arrayInt = String(num).compactMap { $0.wholeNumberValue }.filter { $0 != 0 }.sorted()

        if arrayInt.count < 3 {
            return arrayInt.first! + (arrayInt.count == 1 ? 0 : arrayInt.last!)
        }

        if arrayInt.count == 3 {
            return (arrayInt.first! * 10) + arrayInt[1] + arrayInt[2]
        }

        return (arrayInt[0] * 10 + arrayInt[2]) + (arrayInt[1] * 10 + arrayInt[3])
    }
}
```

---
