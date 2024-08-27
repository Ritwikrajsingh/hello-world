# Merge Two Sorted Lists

### Problime Link: https://leetcode.com/problems/merge-two-sorted-lists/description

## Description

You are given the heads of two sorted linked lists `list1` and `list2`.

Merge the two lists into one **sorted** list. The list should be made by splicing together the nodes of the first two lists.

Return _the head of the merged linked list_.

**Example 1:**

![Input: list1 = [1,2,4], list2 = [1,3,4], Output: [1,1,2,3,4,4]](https://assets.leetcode.com/uploads/2020/10/03/merge_ex1.jpg "Input: list1 = [1,2,4], list2 = [1,3,4], Output: [1,1,2,3,4,4]")

> **Input:** list1 = [1,2,4], list2 = [1,3,4] <br> **Output:** [1,1,2,3,4,4]

**Example 2:**

> **Input:** list1 = [], list2 = [] <br> **Output:** []

**Example 3:**

> **Input:** list1 = [], list2 = [0] <br> **Output:** [0]

**Constraints:**

-   The number of nodes in both lists is in the range `[0, 50]`.
-   `-100 <= Node.val <= 100`
-   Both `list1` and `list2` are sorted in **non-decreasing** order.

## Solutions

### Solution 1: Iterative Method [While Loop]

_We create a `dummyNode` and iterate through both lists, attaching the smaller node to the result each time. Remaining nodes (if any) are added directly._

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
    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
	    ListNode dummyHead = new ListNode();
	    ListNode cur = dummyHead;
		while (list1 != null && list2 != null) {
			if (list1.val <= list2.val) {
				cur.next = list1;
				list1 = list1.next;
			} else {
				cur.next = list2;
				list2 = list2.next;
			}
			cur = cur.next;
		}

		// if (list1 == null) cur.next = list2;
		// if (list2 == null) cur.next = list1;

		cur.next = list1 != null ? list1 : list2;

		return dummyHead.next;
    }
}
```

#### Complexity Analysis

<u>Time Complexity</u>: **O(n)**

-   We traverse each node once.

<u>Space Complexity</u>: **O(1)**

-   No new list is created, just pointer manipulations.

---

### Solution 2: Recursive Method

_We recursively compare the heads of the two lists, and attach the smaller node to the merged result of the remaining list._

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
    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
        if (list1 == null) return list2;
        if (list2 == null) return list1;

        // first approach
        // if (list1.val <= list2.val) {
        //     list1.next = mergeTwoLists(list1.next, list2);
        //     return list1;
        // }
        // list2.next = mergeTwoLists(list1, list2.next);
        // return list2;

        // cleaner approach
        if (list2.val <= list1.val) {
            ListNode list2ref = list2;
            list2 = list1;
            list1 = list2ref;
        }
        list1.next = mergeTwoLists(list1.next, list2);
        return list1;
    }
}
```

#### Complexity Analysis

<u>Time Complexity</u>: **O(n)**

-   Each recursive call processes one node.

<u>Space Complexity</u>: **O(n)**

-   Stack space due to recursion.

---
