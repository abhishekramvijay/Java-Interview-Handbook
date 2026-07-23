# Data Structures & Algorithms (DSA)

> This chapter focuses on interview-oriented problem-solving patterns rather than individual problems. Senior backend interviews typically test your ability to quickly identify the underlying pattern and apply the right algorithm efficiently.

---

# Must Revise (★★★★★)

- Arrays
- Strings
- Hashing
- Two Pointers
- Sliding Window
- Binary Search
- Trees
- Graphs
- Heap
- Dynamic Programming

---

# Contents

1. DSA Interview Strategy
2. Complexity Analysis
3. Arrays
4. Strings
5. Hashing
6. Two Pointers
7. Sliding Window
8. Binary Search

---

# DSA Interview Strategy ★★★★★

Almost every coding interview question follows a common pattern.

```
Understand Problem

↓

Identify Pattern

↓

Choose Data Structure

↓

Write Solution

↓

Optimize

↓

Discuss Complexity
```

Don't memorize solutions.

Recognize the pattern first.

---

# Time Complexity ★★★★★

| Complexity | Example |
|------------|----------|
| O(1) | HashMap Lookup |
| O(log n) | Binary Search |
| O(n) | Linear Scan |
| O(n log n) | Merge Sort |
| O(n²) | Nested Loops |
| O(2ⁿ) | Backtracking |
| O(n!) | Permutations |

---

# Space Complexity ★★★★☆

| Complexity | Example |
|------------|----------|
| O(1) | Variables only |
| O(log n) | Recursion Stack |
| O(n) | HashMap, Queue |
| O(n²) | Matrix |

---

# Pattern 1 — Arrays ★★★★★

## Recognition

Look for

- Maximum / Minimum
- Prefix / Suffix
- Rearrangement
- Interval problems
- Continuous elements

## Core Idea

- Traverse once whenever possible.
- Precompute when repeated calculations are needed.
- Sort only if it simplifies the solution.

## Common Techniques

- Traversal
- Prefix Sum
- Suffix Sum
- Sorting
- Greedy

## Complexity

Usually

```
Time : O(n)

Space : O(1)
```

## Representative Problems

- Two Sum
- Best Time to Buy & Sell Stock
- Product Except Self
- Rotate Array
- Merge Intervals

## Common Mistakes

- Nested loops without necessity.
- Ignoring edge cases.
- Modifying input unnecessarily.

## Interview Signals

✓ Maximum

✓ Minimum

✓ Interval

✓ Prefix Sum

---

# Pattern 2 — Strings ★★★★★

## Recognition

Look for

- Substring
- Palindrome
- Pattern Matching
- Character Frequency

## Core Idea

Convert string problems into

- Two Pointers
- Sliding Window
- HashMap

whenever possible.

## Common Techniques

- Character Count
- Frequency Array
- HashMap
- Two Pointers
- Sliding Window

## Complexity

Most solutions

```
Time : O(n)

Space : O(1) / O(n)
```

## Representative Problems

- Valid Anagram
- Longest Common Prefix
- Longest Palindrome
- Group Anagrams
- String Compression

## Common Mistakes

- Using String concatenation in loops.
- Ignoring case sensitivity.
- Forgetting Unicode considerations.

## Interview Signals

✓ Substring

✓ Palindrome

✓ Frequency

✓ Character Count

---

# Pattern 3 — Hashing ★★★★★

## Recognition

Think HashMap immediately when you hear

- Duplicate
- Frequency
- Lookup
- Pair Search
- Visited Elements

## Core Idea

Trade extra memory for faster lookup.

## Data Structures

- HashMap
- HashSet

## Complexity

```
Lookup : O(1)

Insert : O(1)

Delete : O(1)
```

Average case.

## Representative Problems

- Two Sum
- Contains Duplicate
- Happy Number
- Longest Consecutive Sequence
- Top K Frequent Elements

## Common Mistakes

- Mutable keys.
- Incorrect equals/hashCode.
- Forgetting null handling.

## Interview Signals

✓ Duplicate

✓ Frequency

✓ Fast Lookup

✓ Pair Search

---

# Pattern 4 — Two Pointers ★★★★★

## Recognition

Usually involves

- Sorted array
- Opposite ends
- In-place modification
- Palindrome

## Core Idea

Move one or both pointers based on the condition instead of using nested loops.

## Template

```
left = 0

right = n - 1

while(left < right){

    ...
}
```

## Complexity

```
Time : O(n)

Space : O(1)
```

## Representative Problems

- Two Sum II
- Container With Most Water
- Valid Palindrome
- Remove Duplicates
- Move Zeroes

## Common Mistakes

- Incorrect pointer movement.
- Infinite loop.
- Forgetting sorted-array assumption.

## Interview Signals

✓ Sorted

✓ Pair

✓ Opposite Ends

✓ Palindrome

---

# Pattern 5 — Sliding Window ★★★★★

## Recognition

Look for

- Longest
- Smallest
- Continuous Subarray
- Continuous Substring
- At Most K
- Exactly K

## Core Idea

```
Expand Window

↓

Check Condition

↓

Shrink Until Valid

↓

Update Answer
```

## Data Structures

- Two Pointers
- HashMap
- HashSet
- Frequency Array

## Complexity

Usually

```
Time : O(n)

Space : O(k)
```

## Representative Problems

- Longest Substring Without Repeating Characters
- Minimum Window Substring
- Maximum Consecutive Ones
- Fruit Into Baskets

## Common Mistakes

- Forgetting to shrink.
- Updating answer too early.
- Not maintaining frequency correctly.

## Interview Signals

✓ Longest Substring

✓ Continuous

✓ At Most K

✓ Exactly K

---

# Pattern 6 — Binary Search ★★★★★

## Recognition

Binary Search is applicable whenever

- Data is sorted.
- Search space is monotonic.
- Need minimum feasible answer.
- Need maximum feasible answer.

## Core Idea

```
Calculate Mid

↓

Discard Half

↓

Repeat
```

## Variants

- Classic Binary Search
- First/Last Occurrence
- Binary Search on Answer

## Complexity

```
Time : O(log n)

Space : O(1)
```

## Representative Problems

- Binary Search
- Search Rotated Array
- First Bad Version
- Find Peak Element
- Koko Eating Bananas

## Common Mistakes

- Mid overflow.
- Wrong boundary updates.
- Infinite loops.

## Interview Signals

✓ Sorted

✓ Search

✓ Minimum Possible

✓ Maximum Possible

✓ Monotonic Answer

---

# Pattern Recognition Cheat Sheet ★★★★★

| Keywords | Pattern |
|----------|----------|
| Duplicate | HashMap |
| Frequency | HashMap |
| Sorted | Two Pointers / Binary Search |
| Continuous Subarray | Sliding Window |
| Continuous Substring | Sliding Window |
| Maximum / Minimum | Arrays |
| Pair Search | Two Pointers / HashMap |
| Monotonic Answer | Binary Search |

---

# Frequently Asked Questions

1. Sliding Window vs Two Pointers.
2. HashMap vs HashSet.
3. Binary Search on Answer.
4. Prefix Sum vs Sliding Window.
5. How do you identify the correct pattern?
6. When should sorting be used?
7. How do you optimize a brute-force solution?

---

# DSA Quick Revision

### Arrays
- Prefix Sum
- Suffix Sum
- Sorting
- Greedy

### Strings
- Character Count
- Sliding Window
- Two Pointers

### Hashing
- Duplicate
- Frequency
- Lookup
- Pair Search

### Two Pointers
- Sorted Arrays
- Opposite Ends
- In-place

### Sliding Window
- Longest
- Smallest
- Continuous
- At Most K
- Exactly K

### Binary Search
- Sorted
- Monotonic
- First/Last
- Search Space

### Golden Rule

Recognize the pattern first.

The algorithm usually becomes obvious after that.
