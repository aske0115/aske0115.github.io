# Leetcode [Array] 540. Single Element in a Sorted Array [Medium]

생성일: February 21, 2023 8:01 PM

---

**540. Single Element in a Sorted Array [Medium]**

---

You are given a sorted array consisting of only integers where every element appears exactly twice, except for one element which appears exactly once.

Return *the single element that appears only once*.

Your solution must run in `O(log n)` time and `O(1)` space.

**Example 1:**

```
Input: nums = [1,1,2,3,3,4,4,8,8]
Output: 2

```

**Example 2:**

```
Input: nums = [3,3,7,7,10,11,11]
Output: 10

```

**Constraints:**

- `1 <= nums.length <= 105`
- `0 <= nums[i] <= 105`

---

- **문제 설명**

> 주어진 배열에서 중복되지 않는 값을 리턴하는 문제입니다.
> 

---

- **문제 풀이**

> Binary Search로 풀어야 하는것 같지만, swift에서는 아래와 같이 간단하게도 풀이가 가능합니다.
> 

> Dictionary uniquingKeysWith를 이용하여 배열에서 각 값들의 빈도수를 구하고, 구한 빈도수 중에 빈도수가 1인 값을 찾아 리턴해주도록 하였습니다.
> 

---

### Swift로 작성한 코드는 아래와 같습니다.

```swift
class Solution {
    func singleNonDuplicate(_ nums: [Int]) -> Int {
        Dictionary(nums.map { ($0, 1) }, uniquingKeysWith: +).filter { $0.value == 1 }.first!.key
    }
}
```

---
