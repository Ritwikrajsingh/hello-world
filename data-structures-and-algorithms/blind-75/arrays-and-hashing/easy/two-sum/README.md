# Two Sum

### Problime Link: https://leetcode.com/problems/two-sum/description

## Description

Given an array of integers `nums` and an integer `target`, return _indices of the two numbers such that they add up to `target`_.
You may assume that each input would have **_exactly_ one solution**, and you may not use the _same_ element twice.
You can return the answer in any order.

**Example 1:**

> **Input:** nums = [2,7,11,15], target = 9 <br> **Output:** [0,1] <br>**Explanation:** Because nums[0] + nums[1] == 9, we return [0, 1].

**Example 2:**

> **Input:** nums = [3,2,4], target = 6 <br> **Output:** [1,2]

**Example 3:**

> **Input:** nums = [3,3], target = 6 <br> **Output:** [0,1]

**Constraints:**

-   `2 <= nums.length <= 104`
-   `-109 <= nums[i] <= 109`
-   `-109 <= target <= 109`
-   **Only one valid answer exists.**

## Solutions

### Solution 1: Brute Force

_This solution uses a nested loop to check all pairs of elements in the array. It returns the indices of the first pair that adds up to the target. If no such pair exists, it returns `null`._

#### Python3

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        for first in range(len(nums) - 1):
            for second in range(first + 1, len(nums)):
                if nums[first] + nums[second] == target: return [first, second]
```

#### Java

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        for (int i = 0; i < nums.length - 1; i++) {
            for (int j = i + 1; j < nums.length; j++) {
                if (nums[i] + nums[j] == target) {
                    return new int[] {i, j};
                }
            }
        }
        return null;
    }
}
```

#### Complexity Analysis

<u>Time Complexity</u>: **O(n²)**

-   The outer loop runs n times and the inner loop runs up to n-1 times.
-   In the worst case, every pair of elements is checked once.

<u>Space Complexity</u>: **O(1)**

-   No additional space is used other than a fixed-size array to return the result.

---

### Solution 2: Hash Map

_This approach uses a hash map to store each number and its index as we iterate through the array. For each element, we check whether its complement (i.e., `target - nums[i]`) has already been seen. If it has, we return the indices immediately._

#### Python3

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        map = {}
        for i in range(len(nums)):
            if target - nums[i] in map: return [map[target - nums[i]], i]
            map[nums[i]] = i
```

#### Java

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap < Integer, Integer > map = new HashMap < > ();
        for (int i = 0; i < nums.length; i++) {
            if (map.containsKey(target - nums[i])) {
                return new int[] { map.get(target - nums[i]), i };
            }
            map.put(nums[i], i);
        }
        return null;
    }
}
```

#### Complexity Analysis

<u>Time Complexity</u>: **O(n)**

-   The list is traversed once.
-   Each lookup and insertion in the hash map takes `O(1)` time on average.

<u>Space Complexity</u>: **O(n)**

-   In the worst case, the hash map stores all `n` elements of the array.

---
