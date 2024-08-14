# Valid Anagram

### Problem Link: https://leetcode.com/problems/valid-anagram/description

## Description

Given two strings `s` and `t`, return `true` if `t` is an anagram of `s`, and `false` otherwise.

**Example 1:**

> **Input:** s = "anagram", t = "nagaram" <br> **Output:** true

**Example 2:**

> **Input:** s = "rat", t = "car" <br> **Output:** false

**Constraints:**

-   `1 <= s.length, t.length <= 5 * 10^4`
-   `s` and `t` consist of lowercase English letters.

## Solutions

### Solution 1: Brute Force (Character Matching + Removal)

_For each character in `s`, try to find and remove it in `t`. If any character is not found, return false._

#### Python3

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t): return False # Base Case

        for c in s:
            if c not in t: return False
            t = t.replace(t[t.index(c)], "", 1)

        return len(t) == 0
```

#### Java

```java
class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) return false;

        StringBuilder sBuilder = new StringBuilder(s);

        for (int i = 0; i < t.length(); i++){
            char c = t.charAt(i);
            int index = sBuilder.indexOf(String.valueOf(c));

            if (index != -1) {
                sBuilder.deleteCharAt(index);
            } else {
                return false;
            }
        }

        return sBuilder.length() == 0;
    }
}
```

#### Complexity Analysis

<u>Time Complexity</u>: **O(n^2)**

-   **Python3**:
    -   Loop runs `n` times (for `c` in `s`)
    -   Each `c` in `t`, `t.index(c)`, and `t.replace(...)` takes `O(n)` (since `t` is a _string_ and scanned each time)
    -   So overall: `O(n) × O(n) = O(n^2)`
-   **Java**:

    -   `indexOf` in `StringBuilder` is `O(n)`
    -   `deleteCharAt` is also `O(n)` (due to shifting characters)
    -   For each of n characters: `O(n × n)`

<u>Space Complexity</u>: **O(n)**

-   **Python3**: Each `replace()` creates a new string of length up to `n`
-   **Java**: `StringBuilder` of length `n` is created

---

### Solution 2: Sort & Compare

_This solution converts both strings into character arrays (or lists), sorts them, and compares the results. If the sorted characters are equal, the strings are anagrams._

#### Python3

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t): return False

        return sorted(s) == sorted(t)
```

#### Java

```java
class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) return false;

        char[] sArray = s.toCharArray();
        char[] tArray = t.toCharArray();

        Arrays.sort(sArray);
        Arrays.sort(tArray);

        return Arrays.equals(sArray, tArray);
    }
}
```

#### Complexity Analysis

<u>Time Complexity</u>: **O(n log n)**

-   Sorting both arrays: **Java/Python** takes `O(n log n)` time due to the sorting algorithm it uses (typically **Timsort**).

<u>Space Complexity</u>: **O(1) or O(n)**

-   **Java:** `O(n)` since two new arrays of size `n` are created from `s` and `t`.

-   **Python3:** `O(1)` or `O(n)`, _depends if we are including the sort space or not_ because, `sorted()` function creates a new sorted list of the characters, which requires `O(n)` space.

---

### Solution 3: Hash Map Counting

_This approach uses a `HashMap` (key:value pair) to count the frequency of characters in one string. It then decrements counts using the second string. If any count goes negative or is missing, the strings are not anagrams._

#### Python3

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t): return False # Base Case

        s_map = {}

        for c in s:
            s_map[c] = s_map.get(c, 0) + 1

        for c in t:
            if c not in s_map or s_map[c] == 0: return False

            s_map[c] -= 1

        return True
```

#### Java

```java
class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) return false;

        HashMap<Character, Integer> sMap = new HashMap();

        for (char c: s.toCharArray()) sMap.put(c, (sMap.getOrDefault(c, 0) + 1));

        for (char c: t.toCharArray()) {
            if (!sMap.containsKey(c) || sMap.get(c) == 0) return false;

            sMap.put(c, sMap.get(c) - 1);
        }
        return true;
    }
}
```

#### Complexity Analysis

<u>Time Complexity</u>: **O(n)**

-   One pass for each string.

<u>Space Complexity</u>: **O(n)**

-   `HashMap` stores up to `n` characters

---

### Solution 4: Fixed-size Array Frequency Count (Optimized for Lowercase)

_In this approach we use an integer array of size 26 to count character frequencies._

> ⚠️ _**Note:** Works only when characters are all lowercase `a-z`._

#### Python3

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t): return False

        count = [0] * 26
        base = ord("a") # Unicode code point integer of characher 'a', i.e. 97

        for i in range(len(s)):
            count[ord(s[i]) - base] += 1
            count[ord(t[i]) - base] -= 1

        for v in count:
            if v != 0: return False

        return True
```

#### Java

```java
class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) return false;

        int[] count = new int[26];

        for (int i = 0; i < s.length(); i++) {
            count[s.charAt(i) - 'a']++;
            count[t.charAt(i) - 'a']--;
        }

        for (int v: count) {
            if (v != 0) return false;
        }

        return true;
    }
}
```

#### Complexity Analysis

<u>Time Complexity</u>: **O(n)**

-   Single pass through both strings
-   One loop over a fixed array of size **26** (constant time)

<u>Space Complexity</u>: **O(1)**

-   The `count` array is fixed-size (**26**) regardless of input length

---
