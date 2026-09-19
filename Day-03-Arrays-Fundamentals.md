# 🔥 DAY 3 — ARRAYS FUNDAMENTALS

> **Goal:** Master the array patterns that form the foundation for almost every later DSA topic.
>
> **Priority:** 🔥 MUST KNOW  
> **Estimated Study Time:** 3–4 hours  
> **Recommended split:** 70% problem solving → 20% concepts → 10% revision

---

# 🎯 Today's Goal

By the end of today, you should be able to:

- Understand what an array is and why it is useful.
- Understand zero-based indexing.
- Create, initialize, access, update, and traverse arrays in Java.
- Use normal `for` loops and enhanced `for` loops correctly.
- Find sum, average, minimum, and maximum.
- Search for an element.
- Count elements satisfying a condition.
- Reverse an array.
- Check whether an array is sorted.
- Find the second-largest element.
- Understand in-place modification.
- Understand the difference between an array's length and its valid indices.
- Recognize when a simple linear scan is enough.
- Understand brute force versus one-pass optimization.
- Handle duplicates, negative numbers, zero, one-element arrays, and boundary conditions.
- Use basic Java array utilities.
- Explain the complexity of common array operations.
- Build a strong foundation for Prefix Sum, Two Pointers, Sliding Window, Binary Search, Sorting, and Hashing.

---

# 📌 Prerequisites

You should understand:

- Java variables and data types.
- `if/else`.
- `for` and `while` loops.
- `%` modulo.
- Basic methods.
- Basic time complexity.
- Day 1 Java fundamentals.
- Day 2 number-processing patterns.

No advanced DSA knowledge is required.

---

# 🔥 Priority

## 🔥 MUST KNOW

Arrays are one of the most frequently used structures in:

- Placement coding assessments.
- LeetCode.
- HackerRank.
- Technical interviews.
- Competitive programming.

You should be able to look at a simple array problem and immediately think:

```text
Can I solve this with one traversal?
```

That question is one of the most important habits in DSA.

---

# 1. 🧑‍🎓 BEGINNER EXPLANATION — WHAT IS AN ARRAY?

An array stores multiple values of the same type in a fixed-size sequence.

Example:

```java
int[] nums = {10, 20, 30, 40, 50};
```

Visualize it as:

```text
Index:    0    1    2    3    4
          -------------------------
Value:   10   20   30   40   50
```

Each value has a position called an **index**.

Java arrays start indexing at:

```text
0
```

not `1`.

---

# 2. WHY DO WE NEED ARRAYS?

Imagine storing five numbers without an array:

```java
int a = 10;
int b = 20;
int c = 30;
int d = 40;
int e = 50;
```

This becomes difficult when the number of values grows.

With an array:

```java
int[] nums = {10, 20, 30, 40, 50};
```

You can process all values using a loop.

```text
Array
  ↓
Many values
  ↓
One variable name
  ↓
Access using index
  ↓
Process using loops
```

---

# 3. IMPORTANT TERMINOLOGY

| Term | Meaning |
|---|---|
| Array | Fixed-size collection of same-type elements |
| Element | One value stored in the array |
| Index | Position of an element |
| Length | Number of elements |
| Traversal | Visiting elements one by one |
| Subarray | Contiguous portion of an array |
| In-place | Modifying the existing array without using another array of comparable size |
| Duplicate | A value appearing more than once |
| Sorted | Elements arranged according to an ordering |

---

# 4. ZERO-BASED INDEXING

For:

```java
int[] arr = {5, 10, 15, 20};
```

the indexes are:

```text
Index:    0    1    2    3
          ----------------
Value:    5   10   15   20
```

Therefore:

```java
arr[0] → 5
arr[1] → 10
arr[2] → 15
arr[3] → 20
```

The last valid index is:

```text
arr.length - 1
```

---

# 5. ⚠️ WHY INDEXING MATTERS

If:

```java
arr.length = 4
```

valid indices are:

```text
0, 1, 2, 3
```

This is invalid:

```java
arr[4]
```

because index `4` does not exist.

Java throws:

```text
ArrayIndexOutOfBoundsException
```

---

# 6. 🧑‍🎓 BEGINNER EXPLANATION — ARRAY CREATION

## Method 1 — Initialize immediately

```java
int[] arr = {10, 20, 30};
```

---

## Method 2 — Create with a fixed size

```java
int[] arr = new int[5];
```

Initially:

```text
[0, 0, 0, 0, 0]
```

For an `int` array, elements are initialized to `0`.

---

## Assign values

```java
arr[0] = 10;
arr[1] = 20;
arr[2] = 30;
```

Now:

```text
[10, 20, 30, 0, 0]
```

---

# 7. ARRAY DEFAULT VALUES

When you create an array using `new`, Java initializes its elements.

| Type | Default |
|---|---|
| `int` | `0` |
| `long` | `0L` |
| `double` | `0.0` |
| `boolean` | `false` |
| `char` | `'\u0000'` |
| Object references | `null` |

For DSA, `int[]` is the most common.

---

# 8. ARRAY ACCESS

Given:

```java
int[] arr = {4, 8, 12, 16};
```

Read:

```java
int x = arr[2];
```

Now:

```text
x = 12
```

Update:

```java
arr[2] = 100;
```

Array becomes:

```text
[4, 8, 100, 16]
```

---

# 9. ARRAY TRAVERSAL

The most important array template:

```java
for (int i = 0; i < arr.length; i++) {

    System.out.println(arr[i]);

}
```

Visual:

```text
[10, 20, 30, 40, 50]
 ↑
 i = 0

[10, 20, 30, 40, 50]
      ↑
      i = 1

[10, 20, 30, 40, 50]
           ↑
           i = 2
```

Continue until:

```text
i = arr.length - 1
```

---

# 10. ENHANCED FOR LOOP

You can also write:

```java
for (int value : arr) {
    System.out.println(value);
}
```

Read it as:

> For every value inside `arr`, assign that value to `value`.

This is useful when you only need the elements.

---

## Normal `for` vs enhanced `for`

| Need | Prefer |
|---|---|
| Need index | Normal `for` |
| Need previous/next position | Normal `for` |
| Need to modify using index | Normal `for` |
| Only need values | Enhanced `for` |
| Simple sum/count | Either |

---

# 11. COMPLEXITY OF ARRAY ACCESS

For:

```java
arr[i]
```

the typical access time is:

```text
O(1)
```

Why?

The array uses indexed memory access, so Java can directly access the requested position.

---

# 12. ARRAY TRAVERSAL COMPLEXITY

For:

```java
for (int i = 0; i < arr.length; i++) {
    System.out.println(arr[i]);
}
```

we inspect every element.

If there are `n` elements:

```text
n operations
```

Therefore:

```text
Time: O(n)
Space: O(1)
```

---

# 13. 🧠 HOW TO RECOGNIZE BASIC ARRAY TRAVERSAL

Think of a linear scan when:

- You need to inspect every element.
- You need a sum.
- You need a count.
- You need a maximum/minimum.
- You need to find an occurrence.
- You need to check a property of every element.

### Keywords / Clues

- "given an array"
- "for each element"
- "count"
- "sum"
- "maximum"
- "minimum"
- "find"
- "check whether"

### Ask Yourself

1. Do I need to inspect every element?
2. Can I solve it in one pass?
3. What information do I need to maintain?
4. Can I avoid creating another array?

---

# 14. EXAMPLE 1 — SUM OF ARRAY

## Problem

Given:

```text
[2, 4, 6, 8]
```

return the sum.

Expected:

```text
20
```

---

## Observation

Maintain:

```text
sum
```

For every element:

```text
sum += element
```

---

## Algorithm

```text
sum = 0

for every element:
    add element to sum

return sum
```

---

## Java

```java
class Solution {

    public int arraySum(int[] nums) {

        int sum = 0;

        for (int i = 0; i < nums.length; i++) {
            sum += nums[i];
        }

        return sum;
    }
}
```

---

## Dry Run

Input:

```text
[2, 4, 6, 8]
```

| Element | Sum |
|---:|---:|
| 2 | 2 |
| 4 | 6 |
| 6 | 12 |
| 8 | 20 |

Answer:

```text
20
```

---

## Complexity

```text
Time: O(n)
Space: O(1)
```

---

## ⚠️ Edge Cases

- Empty array → depends on problem definition; sum is often `0`.
- One element → answer is that element.
- Negative numbers.
- Large values → use `long` if required.

---

# 15. EXAMPLE 2 — FIND MAXIMUM

## Problem

```text
[4, 7, 2, 9, 1]
```

Answer:

```text
9
```

---

## 🐌 Brute Force

You could compare many pairs.

But that repeats work.

---

## 💡 Key Observation

Maintain the best answer seen so far.

```text
maximum
```

Start with the first element.

---

## 🚀 Optimal Approach

```text
maximum = nums[0]

for each remaining element:
    if current > maximum:
        maximum = current

return maximum
```

---

## Java

```java
class Solution {

    public int findMax(int[] nums) {

        int maximum = nums[0];

        for (int i = 1; i < nums.length; i++) {

            if (nums[i] > maximum) {
                maximum = nums[i];
            }
        }

        return maximum;
    }
}
```

---

## Dry Run

```text
[4, 7, 2, 9, 1]
```

Start:

```text
maximum = 4
```

Then:

```text
7 > 4 → maximum = 7
2 > 7 → no
9 > 7 → maximum = 9
1 > 9 → no
```

Answer:

```text
9
```

---

## Complexity

```text
Time: O(n)
Space: O(1)
```

---

# 16. EXAMPLE 3 — FIND MINIMUM

Same pattern, opposite comparison.

```java
class Solution {

    public int findMin(int[] nums) {

        int minimum = nums[0];

        for (int i = 1; i < nums.length; i++) {

            if (nums[i] < minimum) {
                minimum = nums[i];
            }
        }

        return minimum;
    }
}
```

---

# 17. EXAMPLE 4 — COUNT ELEMENTS SATISFYING A CONDITION

## Problem

Count how many elements are even.

```text
[1, 2, 4, 7, 8]
```

Answer:

```text
3
```

---

## Java

```java
class Solution {

    public int countEven(int[] nums) {

        int count = 0;

        for (int x : nums) {

            if (x % 2 == 0) {
                count++;
            }
        }

        return count;
    }
}
```

---

## Complexity

```text
Time: O(n)
Space: O(1)
```

---

# 18. EXAMPLE 5 — LINEAR SEARCH

## Problem

Find whether a target exists.

```text
nums = [4, 8, 2, 7, 5]
target = 7
```

Answer:

```text
true
```

---

## 🧑‍🎓 Beginner Explanation

Start from the first element.

Compare:

```text
4 == 7? no
8 == 7? no
2 == 7? no
7 == 7? yes
```

We can stop immediately.

This is called:

> **Linear Search**

---

## Java

```java
class Solution {

    public boolean contains(int[] nums, int target) {

        for (int i = 0; i < nums.length; i++) {

            if (nums[i] == target) {
                return true;
            }
        }

        return false;
    }
}
```

---

## 🧠 Pattern Recognition

Think linear search when:

- The array is not necessarily sorted.
- You only need to find whether a value exists.
- You need the first occurrence.
- The constraints allow `O(n)`.

---

## Complexity

Worst case:

```text
Time: O(n)
Space: O(1)
```

Best case:

```text
Time: O(1)
```

because the target could be the first element.

---

# 19. SEARCH — RETURN INDEX

Sometimes the question asks for the position.

```java
class Solution {

    public int search(int[] nums, int target) {

        for (int i = 0; i < nums.length; i++) {

            if (nums[i] == target) {
                return i;
            }
        }

        return -1;
    }
}
```

Common convention:

```text
found → index
not found → -1
```

Always follow the problem's required output.

---

# 20. EXAMPLE 6 — REVERSE AN ARRAY

Given:

```text
[1, 2, 3, 4, 5]
```

produce:

```text
[5, 4, 3, 2, 1]
```

---

# 21. 🧑‍🎓 BEGINNER EXPLANATION — TWO ENDS

Use two indices:

```text
left
right
```

Visual:

```text
[1, 2, 3, 4, 5]
 ↑           ↑
left       right
```

Swap:

```text
1 ↔ 5
```

Then move:

```text
left++
right--
```

Now:

```text
[5, 2, 3, 4, 1]
    ↑     ↑
   left right
```

Continue until:

```text
left >= right
```

---

# 22. 🚀 IN-PLACE ARRAY REVERSAL

```java
class Solution {

    public void reverse(int[] nums) {

        int left = 0;
        int right = nums.length - 1;

        while (left < right) {

            int temp = nums[left];
            nums[left] = nums[right];
            nums[right] = temp;

            left++;
            right--;
        }
    }
}
```

---

## Dry Run

Input:

```text
[1, 2, 3, 4, 5]
```

### Step 1

```text
left = 0
right = 4

swap 1 and 5

[5, 2, 3, 4, 1]
```

### Step 2

```text
left = 1
right = 3

swap 2 and 4

[5, 4, 3, 2, 1]
```

### Step 3

```text
left = 2
right = 2

stop
```

Answer:

```text
[5, 4, 3, 2, 1]
```

---

## Complexity

```text
Time: O(n)
Space: O(1)
```

Why?

Each element is involved in at most one swap.

---

# 23. 🐌 BRUTE FORCE → 🚀 OPTIMAL — REVERSE ARRAY

## 🐌 Brute Force

Create another array:

```java
int[] result = new int[nums.length];
```

Then copy values from the end.

This uses:

```text
O(n)
```

extra space.

---

## 🚀 Optimal

Swap elements inside the original array.

```text
left ↔ right
```

This uses:

```text
O(1)
```

extra space.

---

## Transition

```text
New array
   ↓
Uses O(n) extra space
   ↓
Ask: can I modify in-place?
   ↓
Two ends
   ↓
Swap
   ↓
O(1) extra space
```

---

# 24. 🧠 HOW TO RECOGNIZE TWO POINTERS FOR ARRAY REVERSAL

Think two pointers when:

- You need to work from both ends.
- You need to reverse an array.
- You need to compare left/right positions.
- You need an in-place transformation.

### Keywords / Clues

- "reverse in-place"
- "from both ends"
- "left and right"
- "swap"
- "without extra array"

### Ask Yourself

1. Can I maintain a left pointer?
2. Can I maintain a right pointer?
3. What happens when they meet?
4. Can I solve this without another array?

---

# 25. EXAMPLE 7 — CHECK WHETHER ARRAY IS SORTED

Suppose:

```text
[1, 2, 2, 4, 7]
```

is sorted in non-decreasing order.

We need:

```text
arr[i] <= arr[i + 1]
```

for every valid `i`.

---

## Java

```java
class Solution {

    public boolean isSorted(int[] nums) {

        for (int i = 0; i < nums.length - 1; i++) {

            if (nums[i] > nums[i + 1]) {
                return false;
            }
        }

        return true;
    }
}
```

---

## Dry Run

```text
[1, 2, 2, 4, 7]
```

Check:

```text
1 <= 2 → yes
2 <= 2 → yes
2 <= 4 → yes
4 <= 7 → yes
```

Answer:

```text
true
```

For:

```text
[1, 5, 3, 7]
```

At:

```text
5 > 3
```

return:

```text
false
```

---

## Complexity

```text
Time: O(n)
Space: O(1)
```

---

# 26. EXAMPLE 8 — SECOND LARGEST DISTINCT ELEMENT

## Problem

Given:

```text
[10, 5, 20, 8, 20, 15]
```

find the second-largest **distinct** value.

Answer:

```text
15
```

The largest distinct value is:

```text
20
```

The second-largest distinct value is:

```text
15
```

---

# 27. 🐌 BRUTE FORCE

One approach:

```text
1. Sort the array.
2. Start from the end.
3. Skip duplicates.
4. Find the next different value.
```

If sorting is used:

```text
Time: O(n log n)
```

---

# 28. 🚀 ONE-PASS OPTIMIZATION

Maintain:

```text
largest
secondLargest
```

For each value:

```text
If x > largest:
    secondLargest = largest
    largest = x

Else if x < largest and x > secondLargest:
    secondLargest = x
```

This can solve the problem in one traversal.

---

## Java

```java
class Solution {

    public int secondLargest(int[] nums) {

        int largest = Integer.MIN_VALUE;
        int secondLargest = Integer.MIN_VALUE;

        for (int x : nums) {

            if (x > largest) {

                secondLargest = largest;
                largest = x;

            } else if (x < largest && x > secondLargest) {

                secondLargest = x;
            }
        }

        return secondLargest;
    }
}
```

This assumes the problem guarantees at least two distinct values.

---

# 29. DRY RUN — SECOND LARGEST

Input:

```text
[10, 5, 20, 8, 20, 15]
```

Start:

```text
largest = -∞
secondLargest = -∞
```

### `10`

```text
largest = 10
secondLargest = -∞
```

### `5`

```text
5 < 10
secondLargest = 5
```

### `20`

```text
20 > 10

secondLargest = 10
largest = 20
```

### `8`

```text
8 < 20
8 > 10? no
```

No update.

### `20`

Equal to largest.

Do not update.

### `15`

```text
15 < 20
15 > 10
```

So:

```text
secondLargest = 15
```

Answer:

```text
15
```

---

# 30. ⚠️ SECOND-LARGEST EDGE CASES

Consider:

```text
[5]
```

No second distinct value.

Consider:

```text
[5, 5, 5]
```

No second distinct value.

Consider:

```text
[-10, -20, -5]
```

Correct:

```text
second largest = -10
```

Do not initialize largest to `0`, because all values may be negative.

---

# 31. EXAMPLE 9 — MOVE ZEROES TO THE END

Given:

```text
[0, 1, 0, 3, 12]
```

produce:

```text
[1, 3, 12, 0, 0]
```

Important requirement in the standard problem:

> Keep the relative order of non-zero elements.

This is a classic array + two-pointer pattern.

---

# 32. 🧠 KEY OBSERVATION

Maintain a position:

```text
insertPos
```

where the next non-zero value should go.

Scan the array.

Whenever you see a non-zero value:

```text
put it at insertPos
insertPos++
```

Then fill the remaining positions with zero.

---

## Java

```java
class Solution {

    public void moveZeroes(int[] nums) {

        int insertPos = 0;

        for (int x : nums) {

            if (x != 0) {
                nums[insertPos] = x;
                insertPos++;
            }
        }

        while (insertPos < nums.length) {

            nums[insertPos] = 0;
            insertPos++;
        }
    }
}
```

---

## Dry Run

Input:

```text
[0, 1, 0, 3, 12]
```

Non-zero values:

```text
1
3
12
```

Write them from the front:

```text
[1, 3, 12, 3, 12]
```

Then fill remaining positions with zero:

```text
[1, 3, 12, 0, 0]
```

---

## Complexity

```text
Time: O(n)
Space: O(1)
```

---

# 33. PATTERN RECOGNITION — COMPACTING AN ARRAY

Think about a write/insert pointer when:

- You need to move certain values.
- You need to remove/ignore certain elements.
- You must preserve relative order.
- The operation should be in-place.

Examples include:

- Move zeroes.
- Remove duplicates from sorted array.
- Remove a target value.
- Compact valid elements.

---

# 34. EXAMPLE 10 — REMOVE ELEMENT IN-PLACE

Given:

```text
nums = [3, 2, 2, 3]
val = 3
```

After removing occurrences of `3`, the valid prefix should be:

```text
[2, 2]
```

The standard LeetCode problem asks for the number `k` of elements remaining and permits arbitrary values beyond the first `k` positions.

---

## Java

```java
class Solution {

    public int removeElement(int[] nums, int val) {

        int write = 0;

        for (int x : nums) {

            if (x != val) {
                nums[write] = x;
                write++;
            }
        }

        return write;
    }
}
```

---

## Dry Run

```text
nums = [3, 2, 2, 3]
val = 3
```

First:

```text
3 == 3
```

Skip.

Then:

```text
2 != 3
nums[0] = 2
write = 1
```

Next:

```text
2 != 3
nums[1] = 2
write = 2
```

Last:

```text
3 == 3
```

Skip.

Return:

```text
k = 2
```

Valid prefix:

```text
[2, 2]
```

---

# 35. 🧠 PATTERN — READ POINTER + WRITE POINTER

The general structure:

```text
read through every element
        ↓
decide whether to keep it
        ↓
if keep:
    write at writeIndex
    writeIndex++
```

This pattern appears frequently in array problems.

---

# 36. ARRAY VS ARRAYLIST

| Feature | Array | ArrayList |
|---|---|---|
| Size | Fixed | Dynamic |
| Syntax | `int[]` | `ArrayList<Integer>` |
| Access | `arr[i]` | `list.get(i)` |
| Length | `arr.length` | `list.size()` |
| Add at end | Not directly | `list.add(x)` |
| Primitive `int` storage | Yes | Uses `Integer` |
| Common DSA use | Very common | Very common |

---

# 37. JAVA-SPECIFIC ARRAY UTILITIES

Import:

```java
import java.util.Arrays;
```

---

## Print an array

```java
System.out.println(Arrays.toString(arr));
```

Example:

```text
[1, 2, 3]
```

---

## Sort an array

```java
Arrays.sort(arr);
```

Typical complexity for primitive arrays is:

```text
O(n log n)
```

---

## Fill an array

```java
Arrays.fill(arr, 0);
```

---

## Copy an array

```java
int[] copy = Arrays.copyOf(arr, arr.length);
```

---

# 38. ⚠️ `arr.length` VS `s.length()`

Array:

```java
arr.length
```

String:

```java
s.length()
```

This is a classic Java syntax mistake.

---

# 39. ARRAY COPYING — REFERENCE VS COPY

Consider:

```java
int[] a = {1, 2, 3};
int[] b = a;
```

Now:

```text
a
 ↓
[1,2,3]
 ↑
b
```

Both variables refer to the same array.

If:

```java
b[0] = 100;
```

then:

```text
a[0] == 100
```

too.

To create a separate copy:

```java
int[] b = Arrays.copyOf(a, a.length);
```

---

# 40. 🧠 WHY THIS MATTERS IN DSA

Sometimes you think:

```java
int[] copy = arr;
```

means "copy the array."

It does not.

It copies the reference.

This can cause unexpected modifications during:

- Sorting.
- Reversing.
- Backtracking.
- Simulation.
- Testing.

---

# 41. 🧑‍🎓 BEGINNER EXPLANATION — SUBARRAY

A subarray is a **contiguous** portion of an array.

Example:

```text
[1, 2, 3, 4]
```

Valid subarrays include:

```text
[1]
[2]
[3]
[4]

[1,2]
[2,3]
[3,4]

[1,2,3]
[2,3,4]

[1,2,3,4]
```

But:

```text
[1,3]
```

is not a subarray because `1` and `3` are not adjacent.

This concept becomes central on Day 4.

---

# 42. SUBARRAY VS SUBSEQUENCE

| Feature | Subarray | Subsequence |
|---|---|---|
| Must be contiguous? | Yes | No |
| Can skip elements? | No | Yes |
| Example from `[1,2,3]` | `[1,2]` | `[1,3]` |
| Important later | Prefix Sum / Sliding Window | DP / subsequence problems |

Do not confuse these terms.

---

# 43. 🧠 PATTERN RECOGNITION — ARRAY PROBLEM TYPES

When you see an array problem, first classify it.

```text
ARRAY
 |
 +-- Need every element?
 |      ↓
 |    Linear Scan
 |
 +-- Need both ends?
 |      ↓
 |    Two Pointers
 |
 +-- Need contiguous range?
 |      ↓
 |    Prefix Sum / Sliding Window
 |
 +-- Sorted + search?
 |      ↓
 |    Binary Search
 |
 +-- Frequency?
 |      ↓
 |    HashMap
 |
 +-- Duplicates?
 |      ↓
 |    HashSet / Two Pointers if sorted
 |
 +-- Need ordering?
        ↓
      Sorting
```

Do not blindly apply a pattern.

Always inspect the problem and constraints.

---

# 44. 🐌 BRUTE FORCE → 🚀 OPTIMAL — GENERAL ARRAY THINKING

Suppose a problem asks:

> Find whether an element exists.

A beginner might think:

```text
Compare target with every element.
```

That's already optimal for an unsorted array.

But if the array is sorted, another technique may exist:

```text
Binary Search
```

Therefore:

> **The same problem can require different algorithms depending on the input properties.**

This is a major DSA lesson.

---

# 45. SORTED VS UNSORTED ARRAY

| Situation | Possible approach |
|---|---|
| Unsorted + search | Linear search |
| Sorted + search | Binary search |
| Sorted + pair target | Two pointers may help |
| Need frequencies | HashMap |
| Need duplicates only | HashSet |
| Need contiguous sum | Prefix Sum / Sliding Window |
| Need reorder | Sorting / two pointers |

This table is a preview of future days.

---

# 46. ⚠️ COMMON BEGINNER MISTAKES

## Mistake 1 — Using `<= arr.length`

Wrong:

```java
for (int i = 0; i <= arr.length; i++)
```

Correct:

```java
for (int i = 0; i < arr.length; i++)
```

---

## Mistake 2 — Starting max at zero

Wrong:

```java
int max = 0;
```

For:

```text
[-5, -2, -10]
```

this gives the wrong answer.

Use:

```java
int max = arr[0];
```

when the array is guaranteed non-empty.

---

## Mistake 3 — Assuming an array is sorted

Never use binary search just because the problem involves searching.

Check whether the input is actually sorted.

---

## Mistake 4 — Forgetting empty-array constraints

If:

```text
arr.length == 0
```

then:

```java
arr[0]
```

is invalid.

---

## Mistake 5 — Confusing index and value

For:

```text
[10, 20, 30]
```

```text
i = 1
arr[i] = 20
```

`i` is the index.

`arr[i]` is the value.

---

## Mistake 6 — Modifying the array unintentionally

Remember:

```java
int[] b = a;
```

does not create a new array.

---

## Mistake 7 — Creating unnecessary arrays

If the problem says "in-place," you probably need to modify the original array using `O(1)` extra space.

---

## Mistake 8 — Sorting unnecessarily

Sorting:

```java
Arrays.sort(arr);
```

costs approximately:

```text
O(n log n)
```

Do not sort if a simple `O(n)` scan can solve the problem.

---

# 47. ⚠️ EDGE CASE MASTER LIST

For array problems, test:

### Empty

```text
[]
```

### One element

```text
[5]
```

### Two elements

```text
[5, 3]
```

### All equal

```text
[7, 7, 7, 7]
```

### All negative

```text
[-5, -2, -10]
```

### Contains zero

```text
[0, 1, 0, 2]
```

### Already sorted

```text
[1, 2, 3, 4]
```

### Reverse sorted

```text
[4, 3, 2, 1]
```

### Duplicate values

```text
[2, 2, 3, 3]
```

### Large input

Check whether your algorithm is fast enough.

---

# 48. 📊 CONSTRAINT → ARRAY ALGORITHM

These are guidelines, not absolute rules.

| Constraint / property | Often consider |
|---|---|
| `n` small | Simple loops may be enough |
| `n ≤ 1,000` | `O(n²)` may sometimes work |
| `n ≤ 100,000` | Prefer `O(n log n)` or `O(n)` |
| `n` very large | Look for `O(n)` / `O(log n)` |
| Array sorted | Binary Search / Two Pointers |
| Need contiguous range | Prefix Sum / Sliding Window |
| Need frequency | HashMap |
| Need uniqueness | HashSet |
| Need in-place transformation | Two pointers / write pointer |
| Need global ordering | Sorting |

---

# 49. PATTERN COMPARISON — LINEAR SEARCH VS BINARY SEARCH

| Feature | Linear Search | Binary Search |
|---|---|---|
| Requires sorted data? | No | Usually yes |
| Time | `O(n)` | `O(log n)` |
| Basic idea | Check one by one | Eliminate half |
| Simple | Yes | Requires sorted/monotonic property |
| Use when | Unsorted or small input | Sorted/monotonic search space |

Binary Search is covered later.

---

# 50. PATTERN COMPARISON — ARRAY VS LINKED LIST

| Feature | Array | Linked List |
|---|---|---|
| Random access | `O(1)` | `O(n)` |
| Memory layout | Contiguous conceptually | Node-based |
| Fixed size | Yes | Dynamic structure |
| Insert middle | Expensive due to shifting | Can be efficient with node reference |
| Search | `O(n)` unsorted | `O(n)` |
| DSA importance | Extremely high | Extremely high |

You will study linked lists later.

---

# 51. 🎤 HOW TO EXPLAIN AN ARRAY SCAN IN AN INTERVIEW

> "I first determine whether the array has any useful property such as sorting."

> "Since this array does not provide a property that lets me skip elements, I use a linear scan."

> "During the scan, I maintain the required information, such as a running sum, maximum, count, or current answer."

> "Each element is processed once, so the time complexity is O(n)."

> "I use O(1) auxiliary space because I only maintain a constant number of variables."

For an in-place problem:

> "Because the problem requires an in-place modification, I avoid creating another array and use pointers to rearrange elements inside the existing array."

---

# 52. 🧪 TRY YOURSELF — MINI PRACTICE

## Problem 1

Find the minimum element of:

```text
[8, 3, 10, 2, 6]
```

<details>
<summary>💡 Hint</summary>

Start:

```java
minimum = nums[0]
```

Then compare every remaining element.

</details>

<details>
<summary>✅ Solution</summary>

```java
int minimum = nums[0];

for (int i = 1; i < nums.length; i++) {

    if (nums[i] < minimum) {
        minimum = nums[i];
    }
}

return minimum;
```

Dry run:

```text
minimum = 8
3 < 8 → 3
10 < 3 → no
2 < 3 → 2
6 < 2 → no

Answer = 2
```

Complexity:

```text
Time: O(n)
Space: O(1)
```

</details>

---

## Problem 2

Count how many values are greater than `10`.

```text
[4, 15, 7, 20, 11]
```

<details>
<summary>💡 Hint</summary>

Use a counter.

</details>

<details>
<summary>✅ Solution</summary>

```java
int count = 0;

for (int x : nums) {

    if (x > 10) {
        count++;
    }
}

return count;
```

Answer:

```text
3
```

Complexity:

```text
Time: O(n)
Space: O(1)
```

</details>

---

# 53. 🧪 MINI PRACTICE — TWO POINTERS

## Problem 1

Reverse:

```text
[10, 20, 30, 40]
```

in-place.

<details>
<summary>💡 Hint</summary>

Use:

```text
left = 0
right = length - 1
```

Swap and move inward.

</details>

<details>
<summary>✅ Solution</summary>

```java
int left = 0;
int right = nums.length - 1;

while (left < right) {

    int temp = nums[left];
    nums[left] = nums[right];
    nums[right] = temp;

    left++;
    right--;
}
```

Result:

```text
[40, 30, 20, 10]
```

Complexity:

```text
Time: O(n)
Space: O(1)
```

</details>

---

## Problem 2

Check whether:

```text
[1, 2, 3, 4, 5]
```

is sorted in ascending/non-decreasing order.

<details>
<summary>💡 Hint</summary>

Compare each element with the next one.

</details>

<details>
<summary>✅ Solution</summary>

```java
for (int i = 0; i < nums.length - 1; i++) {

    if (nums[i] > nums[i + 1]) {
        return false;
    }
}

return true;
```

Complexity:

```text
Time: O(n)
Space: O(1)
```

</details>

---

# 54. 🧪 MINI PRACTICE — WRITE POINTER

## Problem 1

Remove all occurrences of `0` while preserving the order of non-zero elements.

Example:

```text
[0, 3, 0, 5, 7]
```

Expected valid prefix:

```text
[3, 5, 7]
```

<details>
<summary>💡 Hint</summary>

Use:

```text
write = 0
```

Whenever the value is non-zero, write it at `write`.

</details>

<details>
<summary>✅ Solution</summary>

```java
int write = 0;

for (int x : nums) {

    if (x != 0) {
        nums[write] = x;
        write++;
    }
}
```

The first `write` positions contain the desired values.

Complexity:

```text
Time: O(n)
Space: O(1)
```

</details>

---

## Problem 2

Remove all occurrences of `5`.

```text
[5, 1, 5, 2, 3]
```

<details>
<summary>💡 Hint</summary>

Keep values where:

```java
x != 5
```

</details>

<details>
<summary>✅ Solution</summary>

```java
int write = 0;

for (int x : nums) {

    if (x != 5) {
        nums[write] = x;
        write++;
    }
}

return write;
```

Valid prefix:

```text
[1, 2, 3]
```

</details>

---

# 55. PRACTICE PROBLEMS

## 🟢 Easy

### 1. Build Array from Permutation

**Platform:** LeetCode  
**Difficulty:** Easy  
**Pattern:** Array indexing  
**Why this pattern:** Reinforces direct array access and mapping indices to values.  
**What you should notice:** The input itself defines where each result value comes from.  
**Expected Complexity:** `O(n)` time, `O(n)` output space

https://leetcode.com/problems/build-array-from-permutation/

---

### 2. Running Sum of 1d Array

**Platform:** LeetCode  
**Difficulty:** Easy  
**Pattern:** Running sum / prefix-style thinking  
**Why this pattern:** Teaches maintaining accumulated state while scanning once.  
**What you should notice:** Each answer depends on the previous accumulated sum.  
**Expected Complexity:** `O(n)` time; `O(1)` extra space if modifying the allowed output array

https://leetcode.com/problems/running-sum-of-1d-array/

---

### 3. Find Numbers with Even Number of Digits

**Platform:** LeetCode  
**Difficulty:** Easy  
**Pattern:** Array traversal + digit counting  
**Why this pattern:** Combines Day 2 digit processing with Day 3 array traversal.  
**What you should notice:** Apply the same number operation independently to each array element.  
**Expected Complexity:** `O(n log V)` where `V` is the magnitude of an element

https://leetcode.com/problems/find-numbers-with-even-number-of-digits/

---

### 4. Search in an Array

**Platform:** HackerRank  
**Difficulty:** Easy  
**Pattern:** Linear search  
**Why this pattern:** Scan the array until the target is found.  
**What you should notice:** If the array is unsorted, there may be no safe way to skip arbitrary elements.  
**Expected Complexity:** `O(n)`

https://www.hackerrank.com/challenges/intro-to-tutorial-challenges/problem

---

### 5. Remove Element

**Platform:** LeetCode  
**Difficulty:** Easy  
**Pattern:** Read pointer + write pointer / in-place compaction  
**Why this pattern:** Teaches how to keep selected values while modifying the original array.  
**What you should notice:** Only the first `k` positions matter in the standard problem.  
**Expected Complexity:** `O(n)` time, `O(1)` extra space

https://leetcode.com/problems/remove-element/

---

### 6. Move Zeroes

**Platform:** LeetCode  
**Difficulty:** Easy  
**Pattern:** Write pointer / in-place array transformation  
**Why this pattern:** Keeps non-zero values in relative order and moves zeroes to the end.  
**What you should notice:** You can solve it without creating another array.  
**Expected Complexity:** `O(n)` time, `O(1)` extra space

https://leetcode.com/problems/move-zeroes/

---

## 🟡 Medium

### 7. Remove Duplicates from Sorted Array

**Platform:** LeetCode  
**Difficulty:** Easy  
**Pattern:** Two pointers / write pointer  
**Why this pattern:** A sorted array allows duplicates to be compacted in-place.  
**What you should notice:** The sorted property is essential.  
**Expected Complexity:** `O(n)` time, `O(1)` extra space

https://leetcode.com/problems/remove-duplicates-from-sorted-array/

---

### 8. Squares of a Sorted Array

**Platform:** LeetCode  
**Difficulty:** Easy  
**Pattern:** Two pointers  
**Why this pattern:** Negative values can have large squares, so compare absolute values from both ends.  
**What you should notice:** Sorting the squares afterward is unnecessary if you use both ends intelligently.  
**Expected Complexity:** `O(n)` time, `O(n)` output space

https://leetcode.com/problems/squares-of-a-sorted-array/

---

### 9. Best Time to Buy and Sell Stock

**Platform:** LeetCode  
**Difficulty:** Easy  
**Pattern:** One-pass minimum tracking / greedy scan  
**Why this pattern:** Maintain the lowest price seen so far and the best profit.  
**What you should notice:** You do not need to try every pair.  
**Expected Complexity:** `O(n)` time, `O(1)` extra space

https://leetcode.com/problems/best-time-to-buy-and-sell-stock/

---

## 🔴 Hard / Challenge

No hard problem is required today.

The important objective is becoming fluent with:

```text
Traversal
Search
Running state
Two pointers
Write pointer
In-place modification
```

---

# 56. PRACTICE ORDER

Follow this order:

```text
Very Easy
   ↓
Basic traversal
   ↓
Running Sum
   ↓
Linear Search
   ↓
Maximum / Minimum
   ↓
Move Zeroes
   ↓
Remove Element
   ↓
Remove Duplicates
   ↓
Squares of Sorted Array
   ↓
Best Time to Buy and Sell Stock
```

---

# 57. 🧠 PATTERN RECOGNITION TEST

Identify the likely pattern before solving.

### 1.

> Find the largest element in an unsorted array.

**Pattern:** Linear scan.

---

### 2.

> Reverse an array in-place.

**Pattern:** Two pointers.

---

### 3.

> Remove all occurrences of a value while preserving the order of the remaining elements.

**Pattern:** Write pointer / in-place compaction.

---

### 4.

> Determine whether an array is sorted.

**Pattern:** Adjacent comparison / linear scan.

---

### 5.

> Find a target in an unsorted array.

**Pattern:** Linear search.

---

### 6.

> Find a target in a sorted array.

**Possible pattern:** Binary Search.

---

### 7.

> Move all zeroes to the end while keeping non-zero order.

**Pattern:** Write pointer / two-pointer-style compaction.

---

### 8.

> Find the maximum profit from one buy and one later sell.

**Pattern:** One-pass minimum tracking.

---

### 9.

> Find duplicate values in an array.

**Possible patterns:** HashSet, sorting, or problem-specific in-place techniques.

---

### 10.

> Find the sum of every contiguous range repeatedly.

**Pattern:** Prefix Sum may be useful.

---

# 58. 📝 DAILY QUIZ — 10 QUESTIONS

## Q1 — MCQ

For:

```java
int[] arr = {10, 20, 30};
```

what is:

```java
arr.length
```

?

A. `2`  
B. `3`  
C. `4`  
D. Depends on the values

---

## Q2 — Output Prediction

```java
int[] arr = {5, 10, 15};

System.out.println(arr[1]);
```

A. `5`  
B. `10`  
C. `15`  
D. Error

---

## Q3 — Complexity

What is the complexity of:

```java
for (int i = 0; i < arr.length; i++) {
    System.out.println(arr[i]);
}
```

A. `O(1)`  
B. `O(log n)`  
C. `O(n)`  
D. `O(n²)`

---

## Q4 — Debugging

What is wrong?

```java
for (int i = 0; i <= arr.length; i++) {
    System.out.println(arr[i]);
}
```

---

## Q5 — Pattern Recognition

Which pattern is naturally suited to reversing an array in-place?

A. HashMap  
B. Two pointers  
C. BFS  
D. Prefix Sum

---

## Q6 — Concept

Why is this dangerous for finding a maximum?

```java
int max = 0;
```

---

## Q7 — Output Prediction

What happens after:

```java
int[] a = {1, 2, 3};
int[] b = a;

b[0] = 100;

System.out.println(a[0]);
```

A. `1`  
B. `100`  
C. Error  
D. `0`

---

## Q8 — Small Coding

Write the condition that checks whether adjacent elements violate non-decreasing order.

---

## Q9 — Complexity

What is the time complexity of reversing an array with two pointers?

A. `O(1)`  
B. `O(log n)`  
C. `O(n)`  
D. `O(n²)`

---

## Q10 — Pattern Recognition

An array is sorted and you need to search for a target efficiently.

Which technique should you investigate?

A. Binary Search  
B. DFS  
C. Stack  
D. Recursion only

---

# 59. 📝 ANSWER KEY

### Q1

**B. `3`**

Length is the number of elements.

---

### Q2

**B. `10`**

Index `1` contains `10`.

---

### Q3

**C. `O(n)`**

Every element is visited once.

---

### Q4

The condition should be:

```java
i < arr.length
```

not:

```java
i <= arr.length
```

---

### Q5

**B. Two pointers**

Use `left` and `right`.

---

### Q6

An array may contain only negative values.

Example:

```text
[-10, -5, -20]
```

The maximum is `-5`, not `0`.

---

### Q7

**B. `100`**

Both variables refer to the same array.

---

### Q8

```java
if (arr[i] > arr[i + 1]) {
    // not sorted
}
```

---

### Q9

**C. `O(n)`**

There are about `n/2` swaps, which is still `O(n)`.

---

### Q10

**A. Binary Search**

When the required sorted/monotonic property is present.

---

# 60. 🔁 QUICK REVISION

## Remember These

```text
Array
↓
Fixed-size indexed collection

First index
↓
0

Last index
↓
arr.length - 1

Access
↓
arr[i]

Length
↓
arr.length

Traversal
↓
for (int i = 0; i < arr.length; i++)

One-pass scan
↓
O(n)

Array access
↓
O(1)
```

---

## Important Templates

### Basic traversal

```java
for (int i = 0; i < arr.length; i++) {

    int value = arr[i];

}
```

### Enhanced traversal

```java
for (int value : arr) {

}
```

### Sum

```java
long sum = 0;

for (int x : arr) {
    sum += x;
}
```

### Maximum

```java
int max = arr[0];

for (int i = 1; i < arr.length; i++) {

    if (arr[i] > max) {
        max = arr[i];
    }
}
```

### Minimum

```java
int min = arr[0];

for (int i = 1; i < arr.length; i++) {

    if (arr[i] < min) {
        min = arr[i];
    }
}
```

### Linear search

```java
for (int i = 0; i < arr.length; i++) {

    if (arr[i] == target) {
        return i;
    }
}

return -1;
```

### Reverse in-place

```java
int left = 0;
int right = arr.length - 1;

while (left < right) {

    int temp = arr[left];
    arr[left] = arr[right];
    arr[right] = temp;

    left++;
    right--;
}
```

### Check sorted

```java
for (int i = 0; i < arr.length - 1; i++) {

    if (arr[i] > arr[i + 1]) {
        return false;
    }
}

return true;
```

### Write pointer

```java
int write = 0;

for (int x : arr) {

    if (condition) {
        arr[write] = x;
        write++;
    }
}
```

---

## Complexity Cheat Sheet

| Operation / Pattern | Typical Complexity |
|---|---:|
| `arr[i]` access | `O(1)` |
| Update `arr[i]` | `O(1)` |
| Full traversal | `O(n)` |
| Linear search | `O(n)` |
| Find max/min | `O(n)` |
| Reverse in-place | `O(n)` |
| Check sorted | `O(n)` |
| `Arrays.sort(int[])` | `O(n log n)` typical |
| Copy entire array | `O(n)` |
| Extra array of size `n` | `O(n)` space |

---

## Recognition Cheat Sheet

| If you see... | Think... |
|---|---|
| Every element | Linear scan |
| Sum/count | Running variable |
| Largest/smallest | Running max/min |
| Find target in unsorted array | Linear search |
| Reverse in-place | Two pointers |
| Work from both ends | Two pointers |
| Remove selected values | Write pointer |
| Keep relative order | Write pointer / stable compaction |
| Sorted + search | Binary Search |
| Sorted + pair relationship | Two Pointers |
| Contiguous range | Prefix Sum / Sliding Window |
| Frequency | HashMap |
| Unique values | HashSet |
| Need global order | Sorting |

---

# 61. 🏠 HOMEWORK

## Must Solve

1. LeetCode — **Running Sum of 1d Array**
2. LeetCode — **Move Zeroes**
3. LeetCode — **Remove Element**
4. LeetCode — **Remove Duplicates from Sorted Array**
5. LeetCode — **Squares of a Sorted Array**
6. Implement maximum and minimum yourself.
7. Implement linear search yourself.
8. Implement in-place array reversal yourself.

## Optional Challenge

9. LeetCode — **Best Time to Buy and Sell Stock**
10. Find the second-largest distinct element in one pass.
11. Check whether an array is a palindrome using two pointers.

---

# 62. DAY-END SELF TEST

Close this file and try to write these without looking:

```text
1. Array declaration
2. Array traversal
3. Enhanced for loop
4. Sum of array
5. Maximum
6. Minimum
7. Linear search
8. Reverse in-place
9. Check sorted
10. Write-pointer compaction
```

Then explain:

```text
Why is arr[i] O(1)?
Why is full traversal O(n)?
Why does reverse use two pointers?
Why can max be found in one pass?
Why is sorting unnecessary for a simple maximum?
Why does int[] b = a NOT create a new array?
```

If you can answer these comfortably, the foundation is working.

---

# 63. 🏠 HOMEWORK TEMPLATE

For every problem, record:

```text
Problem:
Input:
Output:

Observation:

Brute Force:

Why brute force is slow:

Key optimization:

Algorithm:

Java Code:

Dry Run:

Time Complexity:

Space Complexity:

Edge Cases:

Pattern:
```

This habit will become increasingly useful from Day 4 onward.

---

# 64. 🚦 READY FOR DAY 4?

Next comes one of the most important array patterns:

➡️ [Day 4 — Prefix Sum + Subarrays + Kadane](Day-04-Prefix-Sum-Subarrays-Kadane.md)

⬅️ [Previous Day — Number Problems + Patterns](Day-02-Number-Problems-Patterns.md)  
➡️ [Next Day — Prefix Sum + Subarrays + Kadane](Day-04-Prefix-Sum-Subarrays-Kadane.md)

---

# 🎯 FINAL DAY 3 MINDSET

When you receive an array problem, do **not** immediately think about advanced algorithms.

Start here:

```text
ARRAY
  ↓
What exactly is being asked?
  ↓
Do I need every element?
  ↓
Can one scan solve it?
  ↓
What information should I maintain?
  ↓
Do I need an index?
  ↓
Do I need both ends?
  ↓
Do I need to modify in-place?
  ↓
Is the array sorted?
  ↓
Are there duplicates?
  ↓
Are there contiguous ranges?
  ↓
Check constraints
  ↓
Code
  ↓
Dry run
  ↓
Edge cases
  ↓
Complexity
```

The most important Day 3 lesson is:

> **Before searching for a complicated algorithm, check whether a simple linear scan maintains enough information to solve the problem.**

That single habit will help you recognize many easy and medium DSA problems quickly.

---

**End of Day 3**
