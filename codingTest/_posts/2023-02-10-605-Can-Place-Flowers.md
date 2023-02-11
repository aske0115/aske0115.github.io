---
layout: post
title: <Greedy> 605. Can Place Flowers
---


## Leetcode [Greedy] 605. Can Place Flowers
---
You have a long flowerbed in which some of the plots are planted, and some are not. However, flowers cannot be planted in adjacent plots.

Given an integer array flowerbed containing 0's and 1's, where 0 means empty and 1 means not empty, and an integer n, return if n new flowers can be planted in the flowerbed without violating the no-adjacent-flowers rule.

 
```
Example 1:   

Input: flowerbed = [1,0,0,0,1], n = 1   
Output: true   
```
```
Example 2:   

Input: flowerbed = [1,0,0,0,1], n = 2   
Output: false   
 ```
```
Constraints:

1 <= flowerbed.length <= 2 * 104   
flowerbed[i] is 0 or 1.   
There are no two adjacent flowers in flowerbed.   
0 <= n <= flowerbed.length   
```
---
 
> 1의 위치는 나무를 심을 수 없고, 0일 경우 양쪽모두 나무가 없을 때(0 일때) 나무를 심을 수 있습니다.   
> 간단하게 모든 경우의 수를 비교하여 풀어보았습니다.   
> 일단 현재 위치에 나무를 심을 수 있는 상황에서 (0일 때),
> > 1. 맨 처음 혹은 맨 마지막일 경우에는, 바로 옆 나무가 0인지만 확인하고 0이라면 나무를 심고, count를 증가시킨다.
> > 2. 나머지 경우라면, 양쪽이 0일 경우에만 나무를 심고, count를 증가시킨다.
> > 이때 나무를 심었다면, 심은 바로 옆은 0이라도 나무를 심을 수 없기에,  index값을 +2를 해준다.
> 현재 위치에 나무가 이미 심어저 있다면, 
> > 바로 옆으로 이동한다 (index + 1)

> index가 flowerbed.count보다 작을때까지 반복하며, 그 외에 상황은 이미 모든 나무를 심을 자리를 다 지나온 것이기 때문에,   
> 현재까지 심은 나무의 갯수 (count)를 반환한다.   
 ---
 
 > swift 코드로 보면 다음과 같습니다.
 > > _좀 더 최적화를 할 수도 있을 것 같지만, 지금은 Greedy문제의 접근법을 배워가는 단계이므로 생략하였습니다._   
 

~~~swift
class Solution {
    func canPlaceFlowers(_ flowerbed: [Int], _ n: Int) -> Bool {
        var index = 0
        var count = 0
        var flowered = flowerbed

        while flowered.count > index  {
            if flowered[index] == 0 
                   && ((index - 1 >= 0 && index + 1 < flowered.count && flowered[index - 1] == 0 && flowered[index + 1] == 0) 
                   || (index + 1 >= flowered.count && index - 1 >= 0 && flowered[index - 1] == 0) 
                   || (index - 1 < 0 && index + 1 < flowered.count && flowered[index + 1] == 0)
                   || (index - 1 < 0 && index + 1 >= flowered.count))
                {
                    flowered[index] = 1
                    count += 1
                    index += 2
            } else {
                 index += 1
            }
        }
        return count >= n
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
