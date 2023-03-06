# Leetcode [Array] 1539. Kth Missing Positive Number [Easy]

**1539. Kth Missing Positive Number**

---

Given an array `arr` of positive integers sorted in a **strictly increasing order**, and an integer `k`.

Return *the* `kth` ***positive** integer that is **missing** from this array.*

**Example 1:**

```
Input: arr = [2,3,4,7,11], k = 5
Output: 9
Explanation:The missing positive integers are [1,5,6,8,9,10,12,13,...]. The 5th missing positive integer is 9.

```

**Example 2:**

```
Input: arr = [1,2,3,4], k = 2
Output: 6
Explanation:The missing positive integers are [5,6,7,...]. The 2nd missing positive integer is 6.

```

**Constraints:**

- `1 <= arr.length <= 1000`
- `1 <= arr[i] <= 1000`
- `1 <= k <= 1000`
- `arr[i] < arr[j]` for `1 <= i < j <= arr.length`

**Follow up:**

Could you solve this problem in less than O(n) complexity?

---

- **문제 설명**

> 1부터 차례대로 증가되는 양수 배열이 주어지고, k의 값이 주어집니다.
1부터 증가되는 양수중에 arr에 포함되지 않은 값 중 k번째 인덱스에 해당하는 값을 리턴하는 문제입니다.
> 

---

- **문제 풀이**

> 배열을 처음부터 훑으면서 빠진 값을 체크하고 k의 값을 -1 씩 내려주어 k에 해당하는 빠져있는 값을 리턴해주도록 하였습니다.
> 
- arr의 0번째 인덱스부터 시작하여 빠진 값을 체크하고 K의 값을 줄여줍니다.
- value값은 루프를 돌면서 1씩 증가시켜 주어 1보다 큰 양수를 빠짐없이 체크합니다.
- k값이 다 끝난 시점에 value값이 우리가 구해야 할 정답입니다.
- k값이 다 끝나기 전에 arr를 다 훑었다면, 이후로는 1씩 증가하면서 k인덱스를 줄여줍니다.
- 모든 처리가 끝난 후  저장된 result값을 리턴합니다.

---

### swift 코드는 아래와 같습니다.

```swift
class Solution {
    func findKthPositive(_ arr: [Int], _ k: Int) -> Int {
        var arrIndex = 0
        var value = 1
        var kIndex = k
        var result = 0
        while kIndex > 0 {
            if arr.count > arrIndex {
                if arr[arrIndex] > value {
                    result = value
                    kIndex -= 1
                } else {
                    arrIndex += 1
                }
            } else {
                result = value
                kIndex -= 1
            }
            value += 1
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