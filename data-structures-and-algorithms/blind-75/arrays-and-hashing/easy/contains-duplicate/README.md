# Contains Duplicate

### Problem Link: https://leetcode.com/problems/contains-duplicate/description

## Description

Given an integer array `nums`, return `true` if any value appears **at least twice** in the array, and return `false` if every element is distinct.

**Example 1:**

> **Input:** nums = [1,2,3,1] <br> **Output:** true <br> **Explanation:** The element 1 occurs at the indices 0 and 3.

**Example 2:**

> **Input:** nums = [1,2,3,4] <br> **Output:** false <br> **Explanation:** All elements are distinct.

**Example 3:**

> **Input:** nums = [1,1,1,3,3,4,3,2,4,2] <br> **Output:** true

**Constraints:**

-   `1 <= nums.length <= 105`
-   `-109 <= nums[i] <= 109`

## Solutions

### Solution 1: Brute Force

_Compare every pair using nested loops. If any two elements match, return `true`. Otherwise, return `false`._

#### Java

```java
class Solution {
    public boolean containsDuplicate(int[] nums) {
        for (int i = 0; i < nums.length - 1; i++) {
            for (int j = i + 1; j < nums.length; j++) {
                if (nums[i] == nums[j]) return true;
            }
        }
        return false;
    }
}
```

#### Complexity Analysis

<u>Time Complexity</u>: **O(n^2)**

-   Every element is compared with every other element.

<u>Space Complexity:</u> **O(1)**

-   No additional data structures are used.

---

### Solution 2: Sort First, Then Compare Adjacent

_Sort the array and check if any adjacent elements are equal._

#### Java

```java
class Solution {
    public boolean containsDuplicate(int[] nums) {
        Arrays.sort(nums);
        for (int i = 0; i < nums.length - 1; i++) {
            if (nums[i] == nums[i + 1]) return true;
        }
        return false;
    }
}
```

#### Complexity Analysis

<u>Time Complexity</u>: **O(n log n)**

-   `Arrays.sort()` in Java uses **Timsort** for primitives.

<u>Space Complexity:</u> **O(1)**

-   No additional data structures are used.

---

### Solution 3: Hash Set

_Use a `HashSet` to keep track of seen numbers. If a number repeats, return `true`._

#### Java

```java
import java.util.HashSet;

class Solution {
    public boolean containsDuplicate(int[] nums) {
        HashSet set = new HashSet();
        for (int i: nums) {
            if (set.contains(i)) return true;
            set.add(i);
        }
        return false;
    }
}
```

#### Complexity Analysis

<u>Time Complexity</u>: **O(n)**

-   Each lookup and insertion in a `HashSet` is `O(1)` on average.

<u>Space Complexity:</u> **O(n)**

-   In the worst case, all elements are stored in the `HashSet`.

---

### Solution 4: HashMap - alternative to HashSet

_Same idea as using a `HashSet`, but uses a `HashMap` instead to explicitly store counts or presence._

#### Java

```java
class Solution {
    public boolean containsDuplicate(int[] nums) {
        HashMap map = new HashMap();
        for (int i : nums) {
            if (map.containsKey(i)) return true;
            map.put(i,i);
        }
        return false;
    }
}
```

#### Complexity Analysis

<u>Time Complexity</u>: **O(n)**

<u>Space Complexity:</u> **O(n)**

---

### Solution 5: Hash Set Length

_Convert to a set and compare lengths. If lengths differ, duplicates exist._

#### Python

```python
class Solution:
    def containsDuplicate(self, nums: list[int]) -> bool:
        return len(set(nums)) < len(nums)
```

#### Complexity Analysis

<u>Time Complexity</u>: **O(n)**

<u>Space Complexity:</u> **O(n)**

---
