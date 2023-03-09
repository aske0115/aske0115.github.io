# Leetcode [Linked List] 142. Linked List Cycle II [Medium]

**142. Linked List Cycle II**

---

Given the `head` of a linked list, return *the node where the cycle begins. If there is no cycle, return* `null`.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the `next` pointer. Internally, `pos` is used to denote the index of the node that tail's `next` pointer is connected to (**0-indexed**). It is `-1` if there is no cycle. **Note that** `pos` **is not passed as a parameter**.

**Do not modify** the linked list.

**Example 1:**

![https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist.png](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist.png)

```
Input: head = [3,2,0,-4], pos = 1
Output: tail connects to node index 1
Explanation: There is a cycle in the linked list, where tail connects to the second node.

```

**Example 2:**

![https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test2.png](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test2.png)

```
Input: head = [1,2], pos = 0
Output: tail connects to node index 0
Explanation: There is a cycle in the linked list, where tail connects to the first node.

```

**Example 3:**

![https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test3.png](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test3.png)

```
Input: head = [1], pos = -1
Output: no cycle
Explanation: There is no cycle in the linked list.

```

**Constraints:**

- The number of the nodes in the list is in the range `[0, 104]`.
- `105 <= Node.val <= 105`
- `pos` is `1` or a **valid index** in the linked-list.

**Follow up:** Can you solve it using `O(1)` (i.e. constant) memory?

Could you solve this problem in less than O(n) complexity?

---

- **문제 설명**

> - Linked List가 주어지고 해당 list의 head가 주어집니다.
- pos는 입력 매개변수가 아닌, cycle되는 index의 값입니다.
- 주어진 Linked List가 순환되는(cycle) Linked List이면 순환되는 index의 node를 반환합니다.
> 

---

- **문제 풀이**

> -  탐색한 node를 저장하기 위해 hashMap을 사용합니다.
-  내 노드의 다음값과 내 노드 다음다음의 값을 모두 알고있어야 cycle인지 판단할 수 있으므로 hashMap Value값에 tuple을 사용하였습니다.
- node의 next가 없을 떄까지 while문을 돌면서 cycle을 체크합니다.
- 현재 노드가 hashMap에 없으면 hashMap에 현재 노드의 값을 key로 하고, 현재 노드의 다음노드의 값과 현재 노드 다음다음 노드의 값을 tuple로 저장합니다.
- 현재 노드가 hashMap에 이미 있다면, 지금 노드의 값과, 노드 다음노드의 값,. 그리고 노드 다다음 노드의 값이 이미 들어가있는지 판단하고, 이미 들어가있다면 cycle되는 node라고 판단할 수 있으므로 해당 node를 리턴합니다.
- 현재 노드가 hashMap에 이미 있지만, cycle되지 않는다면 현재 노드값을 key로 하는 tuple배열에 현재 노드 다음노드의 값, 현재 노드 다음다음 노드의 값을 추가해줍니다.
> 

- 위 반복문을 도는 중, cycle을 찾았다면 찾은 현재의 node를 리턴해줍니다.
- 위 반복문이 종료될 때까지 cycle 을 찾지 못했다면 nil을 리턴해줍니다.

---

### swift 코드는 아래와 같습니다.

```swift
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     public var val: Int
 *     public var next: ListNode?
 *     public init(_ val: Int) {
 *         self.val = val
 *         self.next = nil
 *     }
 * }
 */

class Solution {
    func detectCycle(_ head: ListNode?) -> ListNode? {
        var hashMap: [Int : [(next: Int?, nextNext: Int?)]] = [:]
        var root: ListNode? = head
        while root != nil {
            if let next = root!.next {
                if let val = hashMap[root!.val] {
                    if val.contains { $0.next == root!.next?.val && $0.nextNext == root!.next?.next?.val } {
                        return root
                    }
                    hashMap[root!.val]! += [(next: root!.next?.val, nextNext: root!.next?.next?.val)]
                } else {
                    hashMap[root!.val] = [(next: root!.next?.val, nextNext: root!.next?.next?.val)]
                }
            }
            root = root?.next
        }
        return nil
    }
}
```

---