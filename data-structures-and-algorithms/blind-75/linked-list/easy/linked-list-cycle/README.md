# Linked List Cycle

### Problime Link: https://leetcode.com/problems/linked-list-cycle/description

## Description

Given `head`, the head of a linked list, determine if the linked list has a cycle in it.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the `next` pointer. Internally, `pos` is used to denote the index of the node that tail's `next` pointer is connected to. **Note that `pos` is not passed as a parameter**.

Return `true` _if there is a cycle in the linked list_. Otherwise, return `false`.

**Example 1:**

![Input: head = [3,2,0,-4], pos = 1, Output: true](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist.png "Input: head = [3,2,0,-4], pos = 1, Output: true")

> **Input:** head = [3,2,0,-4], pos = 1 <br> **Output:** true <br> **Explanation:** There is a cycle in the linked list, where the tail connects to the 1st node (0-indexed).

**Example 2:**

![Input: head = [1,2], pos = 0, Output: true](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test2.png "Input: head = [1,2], pos = 0, Output: true")

> **Input:** head = [1,2], pos = 0 <br> **Output:** true <br> **Explanation:** There is a cycle in the linked list, where the tail connects to the 0th node.

**Example 3:**

![Input: head = [1], pos = -1, Output: false](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test3.png "Input: head = [1], pos = -1, Output: false")

> **Input:** head = [1], pos = -1 <br> **Output:** false <br> **Explanation:** There is no cycle in the linked list.

**Constraints:**

-   The number of the nodes in the list is in the range `[0, 10^4]`.
-   `-10^5 <= Node.val <= 10^5`
-   `pos` is `-1` or a **valid index** in the linked-list.

## Solutions

### Solution 1: Using HashSet

_We keep a `HashSet` of visited nodes. If we see a node again, there's a cycle._

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
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {
        HashSet<ListNode> set = new HashSet();

        while (head != null) {
            if (set.contains(head)) return true;

            set.add(head);
            head = head.next;
        }

        return false;    }
}
```

#### Complexity Analysis

<u>Time Complexity</u>: **O(n)**

-   We may visit each node once.

<u>Space Complexity</u>: **O(n)**

-   We store all visited nodes.

---

### Solution 2: Marking Visited Node Values

_We modify visited nodes by setting their `val` to a special marker (here `Integer.MAX_VALUE` since we know the constrainsts of the `Node.val`). If we see that marker again, a cycle exists._

#### Java

```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {
        while (head != null) {
            if (head.val == Integer.MAX_VALUE) return true;
            head.val = Integer.MAX_VALUE;
            head = head.next;
        }

        return false;
    }
}
```

#### Complexity Analysis

<u>Time Complexity</u>: **O(n)**

<u>Space Complexity</u>: **O(1)**

---

### Solution 3: Floyd’s Cycle Detection (🐢Tortoise and 🐇Hare)

_We use two pointers: `slow` moves one step, `fast` moves two. If a cycle exists, they will meet._

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
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {
        ListNode slow = head, fast = head;

        while (fast != null && fast.next != null ) {
            slow = slow.next;
            fast = fast.next.next;
            if (fast == slow) return true;
        }

        return false;
    }
}
```

#### Complexity Analysis

<u>Time Complexity</u>: **O(n)**

-   At most we visit each node once or twice.

<u>Space Complexity</u>: **O(1)**

-   No extra space is used.

---
