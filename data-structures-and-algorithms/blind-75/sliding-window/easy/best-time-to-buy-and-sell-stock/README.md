# Best Time to Buy and Sell Stock

### Problime Link: https://leetcode.com/problems/best-time-to-buy-and-sell-stock/description

## Description

You are given an array `prices` where `prices[i]` is the price of a given stock on the `ith` day.

You want to maximize your profit by choosing a **single day** to buy one stock and choosing a **different day in the future** to sell that stock.

Return _the maximum profit you can achieve from this transaction_. If you cannot achieve any profit, return `0`.

**Example 1:**

> **Input:** prices = [7,1,5,3,6,4] <br> **Output:** 5 <br> **Explanation:** Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
> Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.

**Example 2:**

> **Input:** prices = [7,6,4,3,1] <br> **Output:** 0 <br> **Explanation:** In this case, no transactions are done and the max profit = 0.

**Constraints:**

-   `  1 <= prices.length <= 10^5`
-   `0 <= prices[i] <= 10^4`

## Solutions

### Solution 1: Brute Force (nested loops)

_Iterate throug `prices`, try every pair of days `(i, j)` where `i < j` and calculate the `maxProfit`._

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
    public int maxProfit(int[] prices) {
        int maxProfit = 0;

        for (int i = 0; i < prices.length; i++){
            for (int j = i + 1; j < prices.length; j++) {
                maxProfit = Math.max(maxProfit, prices[j] - prices[i]);
            }
        }

        return maxProfit;
    }
}
```

#### Complexity Analysis

<u>Time Complexity</u>: **O(n^2)**

-   We are checking **every possible pair** `(i, j)` such that `i < j`.

<u>Space Complexity</u>: **O(1)**

-   `maxProfit` take constant space.

---

### Solution 2: Sliding Window

_Use two pointers to track the buy and sell days while iterating through the array._

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
    public int maxProfit(int[] prices) {
        int i = 0, j = 1, maxProfit = 0;
        while (i < prices.length && j < prices.length) {
            int profit = prices[j] - prices[i];
            maxProfit = Math.max(maxProfit, profit);
            if (profit < 0) i = j; j++;
        }
        return maxProfit;
    }
}
```

#### Complexity Analysis

<u>Time Complexity</u>: **O(n)**

-   We traverse the array only once.

<u>Space Complexity</u>: **O(1)**

-   `i`, `j` and `maxProfit` take constant space.

---
