# Valid Parentheses

### Problime Link: https://leetcode.com/problems/valid-parentheses/description

## Description

Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.  
An input string is valid if:

1.  Open brackets must be closed by the same type of brackets.
2.  Open brackets must be closed in the correct order.
3.  Every close bracket has a corresponding open bracket of the same type.

**Example 1:**

> **Input:** s = "()" <br> **Output:** true

**Example 2:**

> **Input:** s = "()[]{}" <br> **Output:** true

**Example 3:**

> **Input:** s = "(]" <br> **Output:** false

**Constraints:**

-   `1 <= s.length <= 10^4`
-   `s` consists of parentheses only `'()[]{}'`.

## Solutions

### Solution 1: Stack (Brackets Matching)

_We use a `Stack` to track opening brackets. For each closing bracket, we check if the top of the stack is its matching opening bracket. If matched, pop the stack; otherwise, return false. In the end, the stack should be empty._

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
    public boolean isValid(String s) {
        if (s.length() % 2 == 1) return false;

        Stack<Character> stack = new Stack();

        for (char c : s.toCharArray()) {
            if (c == ')' || c == ']' || c == '}') {
                if (stack.isEmpty())
                    return false;
                char top = (char) stack.peek();
                if (((c == ')' && top == '(') ||
                        (c == '}' && top == '{') ||
                        (c == ']' && top == '['))) {
                    stack.pop();
                } else {
                    return false;
                }
            } else {
                stack.push(c);
            }
        }

        return stack.isEmpty();
    }
}

```

#### Complexity Analysis

<u>Time Complexity</u>: **O(n)**

-   We iterate through the string once, and each operation on the stack takes constant time.

<u>Space Complexity</u>: **O(n)**

-   In the worst case, the stack stores all characters (e.g., when the input is all opening brackets).

---
