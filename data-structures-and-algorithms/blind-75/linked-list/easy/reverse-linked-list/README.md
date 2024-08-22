# Reverse Linked List

### Problime Link: https://leetcode.com/problems/reverse-linked-list/description

## Description

Given the `head` of a singly linked list, reverse the list, and return _the reversed list_.

**Example 1:**

![Input: head = [1,2,3,4,5], Output: [5,4,3,2,1]](https://assets.leetcode.com/uploads/2021/02/19/rev1ex1.jpg "Input: head = [1,2,3,4,5], Output: [5,4,3,2,1]")

> **Input:** head = [1,2,3,4,5] <br> **Output:** [5,4,3,2,1]

**Example 2:**

![Input: head = [1,2], Output: [2,1]](https://assets.leetcode.com/uploads/2021/02/19/rev1ex2.jpg "Input: head = [1,2], Output: [2,1]")

> **Input:** head = [1,2] <br> **Output:** [2,1]

**Example 3:**

> **Input:** head = [] <br> **Output:** []

**Constraints:**

-   The number of nodes in the list is the range `[0, 5000]`.
-   `-5000 <= Node.val <= 5000`

## Solutions

### Solution 1: Iterative Method

_We use a `prev` pointer to keep track of the reversed part of the list. We traverse the list once, changing each node's `next` to point to the previous node._

<!-- #### Python3

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        for first in range(len(nums) - 1):
            for second in range(first + 1, len(nums)):
                if nums[first] + nums[second] == target: return [first, second]
``` -->

#### Java

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode reverseList(ListNode head) {
        if (head == null || head.next == null) return head;
        ListNode prev = null;

        while (head != null) {
            ListNode nextRef = head.next;
            head.next = prev;
            prev = head;
            head = nextRef;
        }
        return prev;
    }
}
```

#### Complexity Analysis

<u>Time Complexity</u>: **O(n)**

-   Each node is visited exactly once.

<u>Space Complexity</u>: **O(1)**

-   Only constant extra memory is used (`prev`, `nextRef`).

---

### Solution 2: Recursive Method

_We recursively reach the end of the list, and then reverse pointers as the call stack unwinds, making each node’s `next` point to itself and detaching the original `next`._

<!-- #### Python3

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        for first in range(len(nums) - 1):
            for second in range(first + 1, len(nums)):
                if nums[first] + nums[second] == target: return [first, second]
``` -->

#### Java

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode reverseList(ListNode head) {
        if (head == null) return head;
        return reverse(head);
    }

    private ListNode reverse(ListNode head) {
        ListNode cur = head;
        if (head.next != null) {
            cur = reverse(head.next);
            head.next.next = head;
        }
        head.next = null;
        return cur;
    }
}
```

### Summary of Call Stack Execution

| Call | `head` | Action                            | New Connection    |
| ---- | ------ | --------------------------------- | ----------------- |
| 1    | 1      | call reverse(2)                   |                   |
| 2    | 2      | call reverse(3)                   |                   |
| 3    | 3      | call reverse(4)                   |                   |
| 4    | 4      | call reverse(5)                   |                   |
| 5    | 5      | base case: return 5               |                   |
| 4    | 4      | set 5.next = 4, set 4.next = null | 5 → 4             |
| 3    | 3      | set 4.next = 3, set 3.next = null | 5 → 4 → 3         |
| 2    | 2      | set 3.next = 2, set 2.next = null | 5 → 4 → 3 → 2     |
| 1    | 1      | set 2.next = 1, set 1.next = null | 5 → 4 → 3 → 2 → 1 |

#### Complexity Analysis

<u>Time Complexity</u>: **O(n)**

-   One recursive call per node.

<u>Space Complexity</u>: **O(n)**

-   Call stack grows linearly with the number of nodes (due to recursion).

---

### Solution 3: Stack-Based Method

_This solution uses a `Stack` to reverse the order of nodes. Initially, we traverse the list and push each node onto a `stack`(The top of the stack will be the last node in the original list). Furthermore, we pop nodes from the `stack` one by one and set the `next` pointer of each popped node to the next node popped, until the `stack` is empty. Finally, we set the `next` pointer of the last node to `null`._

#### Java

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 * int val;
 * ListNode next;
 * ListNode() {}
 * ListNode(int val) { this.val = val; }
 * ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode reverseList(ListNode head) {
        if (head == null)
            return head;
        Stack<ListNode> stack = new Stack();

        while (head != null) {
            stack.push(head);
            head = head.next;
        }

        ListNode prev = stack.pop(); // last item of stack
        ListNode cur = prev;

        while (!stack.isEmpty()) {
            cur.next = stack.pop();
            cur = cur.next;
        }

        cur.next = null;

        return prev;
    }
}
```

#### Complexity Analysis

<u>Time Complexity</u>: **O(n)**

-   We traverse the entire list once to push onto the stack and again to pop and rebuild the reversed.

<u>Space Complexity</u>: **O(n)**

-   The stack stores all `n` nodes, resulting in linear extra space usage.

---
