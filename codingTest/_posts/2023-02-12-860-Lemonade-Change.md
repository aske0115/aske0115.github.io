---
layout: post
title: <Greedy> 860. Lemonade Change [Easy]
---


## Leetcode [Greedy] 860. Lemonade Change [Easy] 
---
At a lemonade stand, each lemonade costs $5. Customers are standing in a queue to buy from you and order one at a time (in the order specified by bills). Each customer will only buy one lemonade and pay with either a $5, $10, or $20 bill. You must provide the correct change to each customer so that the net transaction is that the customer pays $5.

 Note that you do not have any change in hand at first.

 Given an integer array bills where bills[i] is the bill the ith customer pays, return true if you can provide every customer with the correct change, or false otherwise.
 
```
Example 1:   

Input: bills = [5,5,5,10,20]
 Output: true
 Explanation:
 From the first 3 customers, we collect three $5 bills in order.
 From the fourth customer, we collect a $10 bill and give back a $5.
 From the fifth customer, we give a $10 bill and a $5 bill.
 Since all customers got correct change, we output true.
```
```
Example 2:   

 Input: bills = [5,5,10,10,20]
 Output: false
 Explanation:
 From the first two customers in order, we collect two $5 bills.
 For the next two customers in order, we collect a $10 bill and give back a $5 bill.
 For the last customer, we can not give the change of $15 back because we only have two $10 bills.
 Since not every customer received the correct change, the answer is false.
 ```
```
Constraints:

 1 <= bills.length <= 105
 bills[i] is either 5, 10, or 20.
```
---
  
**문제 이해**
```
  * 레몬에이드 판매상점에서 $5짜리 레몬에이드를 판매하고 있습니다.
  * 손님은 $5, $10, $20달라짜리만 지불할 수 있습니다.
  * 주문을 차례대로 받으면서 받은돈에서 레몬에이드 값을 제외한 금액을 모두에게 거슬러줄 수 있으면 true, 거슬러줄 수 없다면 false를 리턴합니다.
```
---
  
**문제풀이**
```
  * 잔돈을 줄 필요가 없는 $5를 지불하는 손님의 돈은 계속 잔고에 채워 넣습니다.
  * $5 초과하는 금액을 지불한 손님이 왔을 경우, 거슬러줄 돈이 있는지 확인합니다. 
      (손님의 돈은 $5, $10, $20 3가지 경우라고 했으니 해당 경우의 수만 판단합니다.)
    * 받은 돈에서 거슬러 줄 돈이 있는지 가지고 있는 돈의 가장 큰 돈부터 반복문을 통해 거스름돈을 만들어 냅니다.
      반복문은 다 거슬러주고 남은 돈이 $5거나, 거슬러 줄 돈이 없을 때 종료됩니다.  
      * 받은 돈 : $20일 경우
         - $10를 가지고 있다면, $10을 거슬러 주고, 거슬러 줘야 할 돈에서 -$10을 합니다.
         - $5를 가지고 있다면, $5를 거슬러 주고, 거슬러 줘야 할 돈에서 -$5를 합니다.
         - 거슬러줄 돈이 $10보다 큰데, 가지고 있는 잔돈에서 $10이 없고, $5도 없다면 거슬러 줄 돈이 없기에 false를 리턴합니다.
      * 받은 돈 : $10일 경우
         - $5를 가지고 있다면, $5를 거슬러 주고, 거슬러 줘야 할 돈에서 -$5를 합니다.
         - $5도 없다면 거슬러 줄 돈이 없기에 false를 리턴합니다.
```
 
### swift 코드로 보면 다음과 같습니다.   

~~~swift
class Solution {
    func lemonadeChange(_ bills: [Int]) -> Bool {
        var money: [Int] = []
        
        func hasTen() -> Bool {
            money.contains(10)
        }
        
        func hasFive() -> Bool {
            money.contains(5)
        }
        
        for i in bills {
            if i == 5 {
                money.append(i)
            } else {
                var order = i
                while order != 5 {
                    if hasTen() && order > 10 {
                        money.remove(at: money.firstIndex(where: { $0 == 10 })!)
                        order -= 10
                    } else if hasFive() {
                        money.remove(at: money.firstIndex(where: { $0 == 5 })!)
                        order -= 5
                    } else {
                        return false
                    }
                }
                money.append(i)
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
