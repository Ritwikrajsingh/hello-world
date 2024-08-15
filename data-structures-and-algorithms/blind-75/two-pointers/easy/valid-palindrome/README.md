# Valid Palindrome

### Problime Link: https://leetcode.com/problems/valid-palindrome/description

## Description

A phrase is a **palindrome** if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

Given a string `s`, return `true` _if it is a **palindrome**, or_ `false` _otherwise_.

**Example 1:**

> **Input:** s = "A man, a plan, a canal: Panama" <br> **Output:** true <br> **Explanation:** "amanaplanacanalpanama" is a palindrome.

**Example 2:**

> **Input:** s = "race a car" <br> **Output:** false <br> **Explanation:** "raceacar" is not a palindrome.

**Example 3:**

> **Input:** s = " " <br> **Output:** false <br> **Explanation:** s is an empty string "" after removing non-alphanumeric characters.
> Since an empty string reads the same forward and backward, it is a palindrome.

**Constraints:**

-   `1 <= s.length <= 2 * 10^5`
-   `s` consists only of printable _ASCII_ characters.

## Solutions

### Solution 1: Reverse and Compare

_Check if string is equal to its reverse.._

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
class Solution {
    public boolean isPalindrome(String s) {
        s = s.toLowerCase(); // to ensure uniform character comparison | O(n)

        StringBuilder sBuilder = new StringBuilder();

        for (char c: s.toCharArray()) { // O(n)
            if (Character.isLetterOrDigit(c)) sBuilder.append(c);
        }

        // return string == string.reverse(); // is not checking the contents of the StringBuilder,
        // it's checking object identity — i.e., whether both sides of the == point to the same object in memory.

        // return sBuilder.toString() == sBuilder.reverse().toString();
        // similarly: This compares object references, not the content of the strings.
        // Even though both .toString() calls return strings with the same contents (after reversing twice), they're two different String objects, so == compares memory addresses and says false.

        return sBuilder.toString().equals(sBuilder.reverse().toString());
    }
}
```

#### Complexity Analysis

<u>Time Complexity</u>: **O(n)**

-   One pass to filter characters and one to reverse and compare.

<u>Space Complexity</u>: **O(n)**

-   A new `StringBuilder` is created to store the filtered string.

---

### Solution 2: Two-Pointer Solution

_Use two pointers moving inward to compare only valid alphanumeric characters in a case-insensitive manner._

#### Python3

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        left, right = 0, len(s) - 1

        while left < right:
            while not s[left].isalnum() and left < right:
                left += 1

            while not s[right].isalnum() and right > left:
                right -= 1

            if s[left].lower() != s[right].lower():
                return False

            left += 1
            right -= 1

        return True

```

#### Java

```java
class Solution {
    public boolean isPalindrome(String s) {
        int left = 0, right = s.length() - 1;

        while (left < right) {
            while (left < right && !Character.isLetterOrDigit(s.charAt(left))) {
                left++;
            }

            while (right > left && !Character.isLetterOrDigit(s.charAt(right))) {
                right--;
            }

            if (Character.toLowerCase(s.charAt(left)) != Character.toLowerCase(s.charAt(right))) {
                return false;
            }

            left++;
            right--;
        }

        return true;
    }
}
```

#### Complexity Analysis

<u>Time Complexity</u>: **O(n)**

-   Each character is visited at most once.

<u>Space Complexity:</u> **O(1)**

-   Only two integer pointers are used; no extra storage used.

---
