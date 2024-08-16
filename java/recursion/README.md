# 🧠 Recursion in Java — A Complete Beginner's Guide

## 📌 What is Recursion?

> **Recursion** is a programming technique where a method **calls itself** to solve a smaller part of a bigger problem.

Instead of solving the full problem directly, recursion breaks it into **subproblems**, each smaller than the last, until it reaches a **base case**.

## 🧮 Example to Warm Up

```java
int factorial(int n) {
    if (n == 0) return 1; // base case
    return n * factorial(n - 1); // recursive case
}
```

Calling `factorial(3)` →  
= `3 * factorial(2)`  
= `3 * 2 * factorial(1)`  
= `3 * 2 * 1 * factorial(0)`  
= `3 * 2 * 1 * 1` → `6`

## 🔑 Key Concepts (Fully Explained)

### 1. ✅ **Base Case**

> The simplest input where recursion stops.

Every recursive function **must** have a base case — this prevents **infinite recursion** and **stack overflow**.

```java
if (n == 0) return  1; // in above example
```

### 2. ✅ **Recursive Case**

> The part where the function **calls itself** with a simpler input.

```java
return n * factorial(n - 1); // in above example
```

### 3. ✅ **Call Stack**

> Java uses a **call stack** to keep track of method calls.

Every recursive call is added to the stack until the base case is reached, then **calls are resolved in reverse** order (LIFO — Last In First Out).

🧱 Stack Flow:

```java
factorial(3)
↳ factorial(2)
   ↳ factorial(1)
      ↳ factorial(0) → return 1
```

Then the stack unwinds:

```java
↳ factorial(1) = 1 * 1 = 1
↳ factorial(2) = 2 * 1 = 2
↳ factorial(3) = 3 * 2 = 6
```

### 4. ✅ **Types of Recursion**

| Type               | Description                          | Example           |
| ------------------ | ------------------------------------ | ----------------- |
| **Direct**         | Function calls **itself** directly   | `f() → f()`       |
| **Indirect**       | Function A calls B, and B calls A    | `f() → g() → f()` |
| **Tail Recursion** | Recursive call is **last statement** | Can be optimized  |
| **Head Recursion** | Recursive call happens **first**     | Before processing |

## 🔎 Recursion vs Iteration

| Feature         | Recursion                       | Iteration (Loops)            |
| --------------- | ------------------------------- | ---------------------------- |
| **Code**        | Shorter, elegant                | Verbose but memory-efficient |
| **Performance** | More memory (stack space)       | Less memory                  |
| **Use Case**    | Tree problems, divide & conquer | Counting, looping            |
| **Risk**        | StackOverflowError              | Infinite loop (less fatal)   |

## ☕ Java-Specific Notes

### 🟡 1. **StackOverflowError**

If base case is missing, recursion goes on forever.

```java
Exception in thread "main" java.lang.StackOverflowError
```

### 🟢 2. **Java Doesn’t Optimize Tail Recursion**

-   Some languages (like Scala, Haskell, etc.) optimize tail recursion to save stack space.
-   **Java does NOT**, so tail-recursive functions still consume stack - memory.

### 🟡 3. **Memory Consumption**

-   Every recursive call uses **stack memory** for parameters and local variables.
-   Deep recursion (thousands of levels) can crash if not carefully designed.

## 🎯 When to Use Recursion

-   ✅ Tree/graph problems
-   ✅ Divide-and-conquer algorithms (merge sort, quicksort)
-   ✅ Combinatorics (permutations, combinations)
-   ✅ Mathematical sequences (Fibonacci, factorial)
-   ✅ Backtracking (sudoku, maze, n-queen)
-   ✅ Any problem where the solution depends on solving **smaller versions** of the same problem

## 💡 Recursion Design Pattern

1.  **Identify the base case.**
2.  **Write recursive case.**
3.  **Assume it works for smaller input.**
4.  **Combine result to solve original problem.**

## 🧪 Basic Template

```java
void recursiveMethod(args) {
    if (base case)
        return;
    // do something
    recursiveMethod(smaller args);
}
```

## 📘 Practice Tips for Recursion

-   🔄 **Dry run** with pen & paper to understand flow
-   ⛓️ Trace the **call stack** for small inputs
-   ✅ Always check for **base case first**
-   🔂 Don’t confuse recursive flow with loops — **each call is a new universe**
-   🔢 Use debugger in IDE to step through recursion

## 🔚 Summary Cheat Sheet

| Concept            | Description                           |
| ------------------ | ------------------------------------- |
| Base Case          | Stops the recursion                   |
| Recursive Case     | Function calls itself                 |
| Stack              | Stores active function calls          |
| StackOverflow      | Caused by missing/incorrect base case |
| Tail Recursion     | Recursive call is the last line       |
| Not Tail-Optimized | Java doesn’t optimize tail recursion  |

---
