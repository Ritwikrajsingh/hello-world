# Add Two Numbers

### Problime Link: https://leetcode.com/problems/add-two-numbers/description

## Description

You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order**, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example 1:**

![Input: l1 = [2,4,3], l2 = [5,6,4], Output: [7,0,8]](https://assets.leetcode.com/uploads/2020/10/02/addtwonumber1.jpg "Input: l1 = [2,4,3], l2 = [5,6,4], Output: [7,0,8]")

> **Input:** l1 = [2,4,3], l2 = [5,6,4] <br> **Output:** [7,0,8] <br> **Explanation:** 342 + 465 = 807.

**Example 2:**

> **Input:** l1 = [0], l2 = [0] <br> **Output:** [0]

**Example 3:**

> **Input:** l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9] <br> **Output:** [8,9,9,9,0,0,0,1]

**Constraints:**

-   The number of nodes in each linked list is in the range `[1, 100]`.
-   `0 <= Node.val <= 9`
-   It is guaranteed that the list represents a number that does not have leading zeros.

## Solutions

### Solution 1: Iterative Method

_We iterate through both linked lists just like we would do if we were adding two numbers on paper from right to left. At each step, we extract the digit from each list (or treat it as 0 if the list has ended), add them along with any carry from the previous step, and store the unit digit of this sum in a new node of the result list. The carry is updated as the tens digit of the sum. We move forward in both lists simultaneously, and once both lists are exhausted, if there’s any remaining carry, we add a final node for it. This creates the final sum digit-by-digit from least significant to most significant._

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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode dummyHead = new ListNode(0);
        ListNode cur = dummyHead;
        int carry = 0;

        while (l1 != null || l2 != null) {
            int val1 = l1 != null ? l1.val : 0;
            int val2 = l2 != null ? l2.val : 0;

            int sum = val1 + val2 + carry;
            carry = sum / 10;

            cur.next = new ListNode(sum % 10);
            cur = cur.next;

            if (l1 != null) l1 = l1.next;
            if (l2 != null) l2 = l2.next;
        }

        if (carry > 0) {
            cur.next = new ListNode(carry);
        }

        return dummyHead.next;
    }
}
```

#### Complexity Analysis

<u>Time Complexity</u>: **O(max(N, M))**

<u>Space Complexity</u>: **O(max(N, M))**

-   For the result list

Where **N** and **M** are lengths of `l1` and `l2`

---

### Solution 2: Recursive (Builder)

_We use recursion to mimic the same digit-by-digit addition process but build the result list progressively by attaching new nodes to a dummy node’s `next` pointer. At each recursive call, we extract the current digits from both lists (or use 0 if the list has ended), add them with the carry, store the unit digit of this sum as a new node, and then recursively handle the next digits and updated carry. This continues until both lists are completely processed and there’s no carry left. The dummy node helps manage the list construction cleanly without returning anything from the recursive function._

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
 * int val;
 * ListNode next;
 * ListNode() {}
 * ListNode(int val) { this.val = val; }
 * ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode dummyHead = new ListNode();
        ListNode cur = dummyHead;
        int carry = 0;

        addTwoNumbers(l1, l2, carry, cur);

        return dummyHead.next;
    }

    private void addTwoNumbers(ListNode l1, ListNode l2, int carry, ListNode cur) {
        if (l1 == null && l2 == null && carry == 0) return;

        int val1 = l1 != null ? l1.val : 0;
        int val2 = l2 != null ? l2.val : 0;
        int sum = val1 + val2 + carry;

        cur.next = new ListNode(sum % 10);
        carry = sum / 10;
        cur = cur.next;

        l1 = (l1 != null) ? l1.next : null;
        l2 = (l2 != null) ? l2.next : null;

        addTwoNumbers(l1, l2, carry, cur);
    }
}
```

#### Complexity Analysis

<u>Time Complexity</u>: **O(max(N, M))**

<u>Space Complexity</u>: **O(max(N, M))**

-   recursion + result list

---

### Solution 3: Recursive (Constructor)

_We recursively build the result linked list by directly returning newly created nodes from each recursive call, going from the least significant digit to the most significant. At each step, we take the digits from the current nodes of both lists, add them with the carry, create a new node for the result of `sum % 10`, and recursively set its `next` pointer to the result of the next recursive call that processes the remaining digits and updated carry. This continues until there are no more digits and no carry to process. The final result is formed as the recursive calls return and link nodes together naturally._

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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        return addTwoNumbers(l1, l2, 0);
    }

    private ListNode addTwoNumbers(ListNode l1, ListNode l2, int carry) {
        if (l1 == null && l2 == null && carry == 0)
            return null;

        int val1 = l1 != null ? l1.val : 0, val2 = l2 != null ? l2.val : 0;
        int sum = val1 + val2 + carry;

        l1 = (l1 != null) ? l1.next : null;
        l2 = (l2 != null) ? l2.next : null;

        ListNode newNode = new ListNode(sum % 10);
        newNode.next = addTwoNumbers(l1, l2, sum / 10);

        return newNode;
    }
}
```

#### Complexity Analysis

<u>Time Complexity</u>: **O(max(N, M))**

<u>Space Complexity</u>: **O(max(N, M))**

-   Due to recursive call stack.

---
