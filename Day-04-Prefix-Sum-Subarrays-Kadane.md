# 🔥 DAY 4 — PREFIX SUM + SUBARRAYS + KADANE'S ALGORITHM

> **Goal:** Learn how to solve repeated range-sum and maximum-subarray problems efficiently.
>
> **Priority:** 🔥🔥🔥 VERY HIGH  
> **Estimated Study Time:** 4–5 hours  
> **Recommended split:** 70% problem solving → 20% concepts → 10% revision

---

# 🎯 Today's Goal

By the end of today, you should be able to:

- Understand what a **subarray** is and what contiguous means.
- Distinguish subarray, subsequence, and subset.
- Generate subarrays.
- Calculate the number of subarrays.
- Understand why repeated range-sum calculations become slow.
- Build and use a Prefix Sum array.
- Answer range-sum queries in `O(1)` after preprocessing.
- Understand the `prefix[R + 1] - prefix[L]` formula.
- Handle negative values and possible integer overflow.
- Understand the maximum subarray problem.
- Derive Kadane's Algorithm instead of memorizing it.
- Handle all-negative arrays correctly.
- Compare `O(n³)`, `O(n²)`, and `O(n)` solutions.
- Recognize Prefix Sum, Kadane, and Sliding Window clues.
- Explain both patterns clearly in an interview.

---

# 📌 Prerequisites

You should already know:

- Java variables and data types.
- `if/else`.
- `for` and `while` loops.
- Methods.
- Arrays.
- Array traversal.
- Basic time complexity.
- Nested loops.

You should have completed:

- **Day 1 — Java Basics**
- **Day 2 — Number Problems + Patterns**
- **Day 3 — Arrays Fundamentals**

---

# 🔥 PRIORITY

## 🔥 MUST KNOW

Prefix Sum and Kadane's Algorithm are important for:

- Placement coding rounds.
- Online assessments.
- LeetCode.
- HackerRank.
- Technical interviews.

The central lesson is:

> **Do not repeatedly calculate information that can be precomputed or maintained incrementally.**

---

# 1. 🧑‍🎓 BEGINNER EXPLANATION — WHAT IS A SUBARRAY?

A **subarray** is a contiguous part of an array.

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

[1, 2]
[2, 3]
[3, 4]

[1, 2, 3]
[2, 3, 4]

[1, 2, 3, 4]
```

The elements must stay next to each other.

---

# 2. WHAT DOES CONTIGUOUS MEAN?

Contiguous means:

> **No gaps.**

From:

```text
[10, 20, 30, 40, 50]
```

this is a subarray:

```text
[20, 30, 40]
```

but:

```text
[20, 40]
```

is not a subarray because `30` was skipped.

---

# 3. SUBARRAY VS SUBSEQUENCE VS SUBSET

| Structure | Contiguous? | Can skip elements? |
|---|---:|---:|
| Subarray | Yes | No |
| Subsequence | No | Yes |
| Subset | No | Yes |

Example:

```text
[1, 2, 3]
```

`[1,2]` is a subarray.

`[1,3]` can be a subsequence.

For today's problems, when you see:

> **subarray**

immediately think:

```text
CONTIGUOUS
```

---

# 4. 🧑‍🎓 HOW TO GENERATE SUBARRAYS

Choose:

```text
start
end
```

Every pair satisfying:

```text
start <= end
```

defines a subarray.

For:

```text
[1, 2, 3]
```

```text
start = 0
    end = 0 → [1]
    end = 1 → [1,2]
    end = 2 → [1,2,3]

start = 1
    end = 1 → [2]
    end = 2 → [2,3]

start = 2
    end = 2 → [3]
```

---

# 5. NUMBER OF SUBARRAYS

For an array of length `n`:

```text
Number of subarrays = n × (n + 1) / 2
```

Example:

```text
n = 4

4 × 5 / 2 = 10
```

---

# 6. WHY?

There are:

```text
n + (n-1) + (n-2) + ... + 1
```

possible choices.

Therefore:

```text
n(n+1)/2
```

---

# 7. IMPORTANT CONSEQUENCE

For:

```text
n = 100,000
```

the number of subarrays is enormous.

So explicitly processing every subarray can be too slow.

This motivates:

- Prefix Sum.
- Kadane.
- Sliding Window.
- Prefix Sum + HashMap.

---

# 8. GENERATING ALL SUBARRAYS

Basic enumeration:

```java
for (int start = 0; start < nums.length; start++) {

    for (int end = start; end < nums.length; end++) {

        // subarray = nums[start...end]

    }
}
```

Number of iterations:

```text
O(n²)
```

If you additionally scan every element to calculate each sum, it can become:

```text
O(n³)
```

---

# 9. 🐌 BRUTE FORCE — MAXIMUM SUBARRAY SUM

Problem:

> Find the maximum sum of any contiguous subarray.

Example:

```text
[-2, 1, -3, 4, -1, 2, 1, -5, 4]
```

Answer:

```text
6
```

because:

```text
[4, -1, 2, 1]
```

has sum:

```text
4 - 1 + 2 + 1 = 6
```

---

# 10. BRUTE FORCE

Choose:

```text
start
end
```

then calculate the sum.

Naively:

```text
for start
    for end
        for i from start to end
            sum += nums[i]
```

Complexity:

```text
O(n³)
```

---

# 11. 💡 IMPROVED BRUTE FORCE

Notice:

```text
sum(start, end)
=
sum(start, end-1) + nums[end]
```

So keep a running sum for each `start`.

```java
class Solution {

    public int maxSubArrayBruteForce(int[] nums) {

        int maxSum = Integer.MIN_VALUE;

        for (int start = 0; start < nums.length; start++) {

            int sum = 0;

            for (int end = start; end < nums.length; end++) {

                sum += nums[end];

                maxSum = Math.max(maxSum, sum);
            }
        }

        return maxSum;
    }
}
```

Complexity:

```text
Time: O(n²)
Space: O(1)
```

---

# 12. 🚀 KADANE'S ALGORITHM

Kadane solves maximum subarray sum in:

```text
O(n)
```

Core question:

> **Should I extend the previous subarray or start a new subarray here?**

For each element:

```text
currentSum = max(
    nums[i],
    currentSum + nums[i]
)
```

Then:

```text
maxSum = max(maxSum, currentSum)
```

---

# 13. WHAT DO THE VARIABLES MEAN?

### `currentSum`

The best sum of a subarray that **must end at the current index**.

### `maxSum`

The best sum seen anywhere so far.

Do not confuse these.

---

# 14. JAVA — KADANE

```java
class Solution {

    public int maxSubArray(int[] nums) {

        int currentSum = nums[0];
        int maxSum = nums[0];

        for (int i = 1; i < nums.length; i++) {

            currentSum = Math.max(
                nums[i],
                currentSum + nums[i]
            );

            maxSum = Math.max(maxSum, currentSum);
        }

        return maxSum;
    }
}
```

---

# 15. DRY RUN — KADANE

Input:

```text
[-2, 1, -3, 4, -1, 2, 1, -5, 4]
```

| Value | Current Sum | Max Sum |
|---:|---:|---:|
| -2 | -2 | -2 |
| 1 | 1 | 1 |
| -3 | -2 | 1 |
| 4 | 4 | 4 |
| -1 | 3 | 4 |
| 2 | 5 | 5 |
| 1 | 6 | 6 |
| -5 | 1 | 6 |
| 4 | 5 | 6 |

Answer:

```text
6
```

---

# 16. WHY KADANE WORKS

At each index there are only two useful choices:

```text
START NEW
nums[i]
```

or:

```text
CONTINUE
currentSum + nums[i]
```

Choose the larger.

A negative accumulated sum can hurt a future subarray, so when starting fresh is better, we discard the previous segment.

---

# 17. ⚠️ ALL-NEGATIVE ARRAYS

Consider:

```text
[-8, -3, -6, -2, -5]
```

Correct answer:

```text
-2
```

Do **not** initialize:

```java
int maxSum = 0;
```

because that would incorrectly allow an empty subarray.

Use:

```java
int currentSum = nums[0];
int maxSum = nums[0];
```

when the problem guarantees a non-empty array.

---

# 18. KADANE — ALL NEGATIVE DRY RUN

```text
[-8, -3, -6, -2, -5]
```

Start:

```text
current = -8
best = -8
```

At `-3`:

```text
max(-3, -11) = -3
best = -3
```

At `-6`:

```text
max(-6, -9) = -6
```

At `-2`:

```text
max(-2, -8) = -2
best = -2
```

At `-5`:

```text
max(-5, -7) = -5
```

Final:

```text
-2
```

---

# 19. 🧠 KADANE PATTERN RECOGNITION

Think Kadane when you see:

- Maximum subarray sum.
- Maximum sum of a contiguous segment.
- Best contiguous segment.
- Largest sum from a continuous range.

Ask:

```text
Is it contiguous?
        ↓
Is it asking for maximum/minimum sum?
        ↓
Can I keep the best segment ending here?
        ↓
Kadane
```

---

# 20. BRUTE FORCE → KADANE

```text
O(n³)
   ↓
Avoid recalculating each subarray sum
   ↓
O(n²)
   ↓
Keep only the best subarray ending at each index
   ↓
O(n)
```

The important interview skill is not memorizing Kadane.

It is understanding **why repeated work can be removed**.

---

# 21. 🧑‍🎓 BEGINNER EXPLANATION — PREFIX SUM

Suppose:

```text
nums = [2, 4, 1, 5, 3]
```

and we repeatedly need sums of ranges.

Example:

```text
sum(1,3)
```

means:

```text
4 + 1 + 5 = 10
```

Instead of repeatedly traversing ranges, precompute cumulative sums.

---

# 22. PREFIX SUM IDEA

Use a prefix array with one extra position:

```text
prefix[0] = 0
```

and:

```text
prefix[i + 1] = prefix[i] + nums[i]
```

For:

```text
[2,4,1,5,3]
```

we get:

```text
[0,2,6,7,12,15]
```

---

# 23. PREFIX SUM VISUALIZATION

```text
nums:
Index:   0   1   2   3   4
         -------------------
Value:   2   4   1   5   3

prefix:
Index:   0   1   2   3   4   5
         -----------------------
Value:   0   2   6   7  12  15
```

Meaning:

```text
prefix[1] = nums[0]
prefix[2] = nums[0] + nums[1]
prefix[3] = nums[0] + nums[1] + nums[2]
...
```

---

# 24. WHY THE LEADING ZERO?

It makes range formulas uniform.

For an inclusive range:

```text
nums[L..R]
```

the answer is:

```text
prefix[R + 1] - prefix[L]
```

---

# 25. RANGE SUM EXAMPLE

```text
nums = [2,4,1,5,3]
```

Find:

```text
L = 1
R = 3
```

Directly:

```text
4 + 1 + 5 = 10
```

Prefix:

```text
[0,2,6,7,12,15]
```

Formula:

```text
prefix[4] - prefix[1]
= 12 - 2
= 10
```

---

# 26. WHY SUBTRACTION WORKS

`prefix[R+1]` contains:

```text
nums[0] + ... + nums[L-1] + nums[L] + ... + nums[R]
```

`prefix[L]` contains:

```text
nums[0] + ... + nums[L-1]
```

Subtract them.

Everything before `L` cancels.

Remaining:

```text
nums[L] + ... + nums[R]
```

---

# 27. BUILD PREFIX SUM IN JAVA

```java
class PrefixSum {

    public static int[] buildPrefix(int[] nums) {

        int[] prefix = new int[nums.length + 1];

        for (int i = 0; i < nums.length; i++) {
            prefix[i + 1] = prefix[i] + nums[i];
        }

        return prefix;
    }
}
```

Complexity:

```text
Time: O(n)
Space: O(n)
```

---

# 28. RANGE QUERY IN JAVA

```java
class Solution {

    public int rangeSum(int[] nums, int left, int right) {

        int[] prefix = new int[nums.length + 1];

        for (int i = 0; i < nums.length; i++) {
            prefix[i + 1] = prefix[i] + nums[i];
        }

        return prefix[right + 1] - prefix[left];
    }
}
```

For multiple queries, build the prefix array **once**, not once per query.

---

# 29. PREFIX SUM COMPLEXITY

Build:

```text
O(n)
```

Each query:

```text
O(1)
```

For `q` queries:

```text
O(n + q)
```

Space:

```text
O(n)
```

---

# 30. 🐌 WITHOUT PREFIX SUM

If every query scans:

```text
L → R
```

then repeated overlapping work may produce roughly:

```text
O(nq)
```

in the worst case.

Prefix Sum changes this to:

```text
Build once: O(n)
Each query: O(1)
Total: O(n + q)
```

---

# 31. PREFIX SUM PATTERN RECOGNITION

Think Prefix Sum when you see:

- Range sum.
- Sum from `L` to `R`.
- Multiple sum queries.
- Repeated overlapping sums.
- Cumulative sum.
- Contiguous range sum.

Ask:

```text
Will I repeatedly calculate overlapping sums?
        ↓
Can I precompute cumulative information?
        ↓
Prefix Sum
```

---

# 32. PREFIX SUM WITH NEGATIVE NUMBERS

Prefix Sum works normally with negatives.

Example:

```text
nums = [5, -2, 4, -1]
```

Prefix:

```text
[0,5,3,7,6]
```

Range `[1,3]`:

```text
prefix[4] - prefix[1]
= 6 - 5
= 1
```

Directly:

```text
-2 + 4 - 1 = 1
```

---

# 33. ⚠️ INTEGER OVERFLOW

For large values, `int` may not be enough.

Example:

```text
1,000,000,000
1,000,000,000
1,000,000,000
```

Use:

```java
long[] prefix = new long[nums.length + 1];
```

and:

```java
long
```

when constraints require it.

---

# 34. JAVA LONG PREFIX TEMPLATE

```java
long[] prefix = new long[nums.length + 1];

for (int i = 0; i < nums.length; i++) {
    prefix[i + 1] = prefix[i] + nums[i];
}

long rangeSum = prefix[right + 1] - prefix[left];
```

---

# 35. ⚠️ PREFIX INDEXING MISTAKE

With the leading-zero representation:

Wrong:

```java
prefix[right] - prefix[left]
```

Correct:

```java
prefix[right + 1] - prefix[left]
```

Memorize:

```text
R + 1
```

---

# 36. PREFIX SUM — MULTIPLE QUERIES

Array:

```text
[3,1,4,1,5]
```

Prefix:

```text
[0,3,4,8,9,14]
```

### Query `[0,2]`

```text
prefix[3] - prefix[0]
= 8
```

### Query `[1,4]`

```text
prefix[5] - prefix[1]
= 14 - 3
= 11
```

### Query `[2,3]`

```text
prefix[4] - prefix[2]
= 9 - 4
= 5
```

---

# 37. PREFIX SUM — BRUTE FORCE → OPTIMAL

### Brute Force

For every query:

```text
loop L → R
calculate sum
```

Potential complexity:

```text
O(nq)
```

### Prefix Sum

```text
preprocess → O(n)

query → O(1)
```

Total:

```text
O(n + q)
```

---

# 38. 🧠 GENERAL PRECOMPUTATION PATTERN

The deeper DSA idea is:

```text
Repeated calculation
        ↓
Notice overlapping work
        ↓
Precompute reusable information
        ↓
Answer future queries faster
```

Prefix Sum is one example of this idea.

---

# 39. PREFIX SUM IS NOT FOR EVERYTHING

Do not automatically use Prefix Sum for every subarray problem.

Examples:

```text
Maximum subarray sum
→ Kadane

Maximum sum of exactly k consecutive elements
→ Sliding Window

Sum exactly K
→ Prefix Sum + HashMap may be useful
```

The exact wording and constraints determine the pattern.

---

# 40. KADANE VS PREFIX SUM

| Feature | Prefix Sum | Kadane |
|---|---|---|
| Main purpose | Range sums | Maximum subarray sum |
| Preprocessing | Yes | No |
| Query | `O(1)` | Not a range-query structure |
| Extra space | Usually `O(n)` | `O(1)` |
| Core idea | Cumulative sums | Best ending-at-current sum |
| Key clue | `[L,R]` range sums | Maximum contiguous sum |

---

# 41. PREFIX SUM VS SUBARRAY BRUTE FORCE

| Approach | Time | Extra Space |
|---|---:|---:|
| Triple loop | `O(n³)` | `O(1)` |
| Nested loops + running sum | `O(n²)` | `O(1)` |
| Prefix Sum build | `O(n)` | `O(n)` |
| Prefix Sum query | `O(1)` | Prefix structure required |

---

# 42. KADANE VS BRUTE FORCE

| Approach | Time | Extra Space |
|---|---:|---:|
| Triple loop | `O(n³)` | `O(1)` |
| Nested loops + running sum | `O(n²)` | `O(1)` |
| Kadane | `O(n)` | `O(1)` |

---

# 43. 🧠 PATTERN RECOGNITION MAP

```text
SUBARRAY
   |
   +-- Repeated range sums?
   |       ↓
   |    Prefix Sum
   |
   +-- Maximum contiguous sum?
   |       ↓
   |    Kadane
   |
   +-- Exactly k consecutive elements?
   |       ↓
   |    Sliding Window
   |
   +-- Sum exactly K?
           ↓
      Prefix Sum + HashMap
      (depending on constraints)
```

---

# 44. CONSTRAINT THINKING

Rough guideline:

| Constraint | Usually investigate |
|---|---|
| `n ≤ 100` | Simple `O(n²)` may be fine |
| `n ≤ 1,000` | `O(n²)` may sometimes work |
| `n ≤ 100,000` | Prefer `O(n log n)` or `O(n)` |
| `n ≈ 1,000,000` | Be very careful with `O(n²)` |

Always read the actual problem constraints.

---

# 45. KADANE — RETURNING THE ACTUAL RANGE

Sometimes the problem asks for the actual maximum subarray, not only its sum.

Track:

```text
currentStart
bestStart
bestEnd
```

```java
class Solution {

    public int[] maxSubArrayRange(int[] nums) {

        int currentSum = nums[0];
        int maxSum = nums[0];

        int currentStart = 0;
        int bestStart = 0;
        int bestEnd = 0;

        for (int i = 1; i < nums.length; i++) {

            if (nums[i] > currentSum + nums[i]) {
                currentSum = nums[i];
                currentStart = i;
            } else {
                currentSum += nums[i];
            }

            if (currentSum > maxSum) {
                maxSum = currentSum;
                bestStart = currentStart;
                bestEnd = i;
            }
        }

        return new int[]{bestStart, bestEnd};
    }
}
```

For:

```text
[-2,1,-3,4,-1,2,1,-5,4]
```

the best range is:

```text
[3, 6]
```

corresponding to:

```text
[4,-1,2,1]
```

---

# 46. 🧪 MINI PRACTICE — PREFIX SUM

## Problem 1

Build the Prefix Sum array:

```text
[5,2,7,3,1]
```

<details>
<summary>💡 Hint</summary>

Start with:

```text
prefix[0] = 0
```

</details>

<details>
<summary>✅ Solution</summary>

```text
[0,5,7,14,17,18]
```

Complexity:

```text
Time: O(n)
Space: O(n)
```

</details>

---

## Problem 2

Using:

```text
nums = [5,2,7,3,1]
```

find the sum from index `1` to `3`.

<details>
<summary>💡 Hint</summary>

Use:

```text
prefix[R+1] - prefix[L]
```

</details>

<details>
<summary>✅ Solution</summary>

```text
prefix = [0,5,7,14,17,18]

17 - 5 = 12
```

Direct check:

```text
2 + 7 + 3 = 12
```

</details>

---

# 47. 🧪 MINI PRACTICE — KADANE

## Problem 1

Find the maximum subarray sum:

```text
[-2,3,-1,2,-5]
```

<details>
<summary>💡 Hint</summary>

At each position choose:

```text
start here
OR
continue
```

</details>

<details>
<summary>✅ Solution</summary>

The best subarray is:

```text
[3,-1,2]
```

Sum:

```text
4
```

Complexity:

```text
O(n) time
O(1) space
```

</details>

---

## Problem 2

Find the maximum subarray sum:

```text
[-8,-3,-6,-2,-5]
```

<details>
<summary>💡 Hint</summary>

Do not initialize the answer to zero.

</details>

<details>
<summary>✅ Solution</summary>

The best non-empty subarray contains:

```text
[-2]
```

Answer:

```text
-2
```

</details>

---

# 48. 🧪 MINI PRACTICE — SUBARRAY COUNTING

How many subarrays are there in:

```text
[1,2,3,4,5]
```

<details>
<summary>💡 Hint</summary>

Use:

```text
n(n+1)/2
```

</details>

<details>
<summary>✅ Solution</summary>

```text
5 × 6 / 2 = 15
```

Answer:

```text
15
```

</details>

---

# 49. FULL PRACTICE — RANGE SUM QUERIES

Given:

```text
nums = [2,4,1,5,3]
```

queries:

```text
[0,2]
[1,3]
[2,4]
```

### Brute Force

```text
[0,2] → 2+4+1 = 7
[1,3] → 4+1+5 = 10
[2,4] → 1+5+3 = 9
```

### Prefix Sum

```text
prefix = [0,2,6,7,12,15]
```

```text
[0,2] → prefix[3] - prefix[0] = 7
[1,3] → prefix[4] - prefix[1] = 10
[2,4] → prefix[5] - prefix[2] = 9
```

Java:

```java
class RangeSumQuery {

    private final long[] prefix;

    public RangeSumQuery(int[] nums) {

        prefix = new long[nums.length + 1];

        for (int i = 0; i < nums.length; i++) {
            prefix[i + 1] = prefix[i] + nums[i];
        }
    }

    public long rangeSum(int left, int right) {
        return prefix[right + 1] - prefix[left];
    }
}
```

Complexity:

```text
Construction: O(n)
Each query: O(1)
Space: O(n)
```

---

# 50. FULL PRACTICE — MAXIMUM SUBARRAY

Input:

```text
[-2,1,-3,4,-1,2,1,-5,4]
```

Output:

```text
6
```

### Brute Force

Check all subarrays.

With a running sum:

```text
O(n²)
```

### Observation

For each index, only the best subarray ending there matters.

### Kadane

```java
class Solution {

    public int maxSubArray(int[] nums) {

        int currentSum = nums[0];
        int maxSum = nums[0];

        for (int i = 1; i < nums.length; i++) {

            currentSum = Math.max(
                nums[i],
                currentSum + nums[i]
            );

            maxSum = Math.max(maxSum, currentSum);
        }

        return maxSum;
    }
}
```

Dry-run state:

```text
current:
-2 → 1 → -2 → 4 → 3 → 5 → 6 → 1 → 5

best:
-2 → 1 → 1 → 4 → 4 → 5 → 6 → 6 → 6
```

Answer:

```text
6
```

Complexity:

```text
Time: O(n)
Space: O(1)
```

---

# 51. ⚠️ COMMON BEGINNER MISTAKES — PREFIX SUM

### Mistake 1 — Forgetting the extra position

For the standard convention:

```java
new int[n + 1]
```

### Mistake 2 — Wrong formula

Wrong:

```java
prefix[right] - prefix[left]
```

Correct:

```java
prefix[right + 1] - prefix[left]
```

### Mistake 3 — Rebuilding Prefix Sum for every query

Build once.

### Mistake 4 — Ignoring overflow

Use `long` when constraints require it.

---

# 52. ⚠️ COMMON BEGINNER MISTAKES — KADANE

### Mistake 1

```java
maxSum = 0;
```

Fails for all-negative arrays.

### Mistake 2

Thinking:

```text
currentSum = global answer
```

It is not.

### Mistake 3

Forgetting that the subarray must be contiguous.

### Mistake 4

Using Kadane when the problem asks for a fixed-size window or a range query.

---

# 53. EDGE CASE MASTER LIST

Test today's algorithms with:

```text
[]
[7]
[-7]
[-5,-2,-9]
[1,2,3,4]
[-2,5,-1,4,-3]
[0,0,0]
```

For range queries also test:

```text
L = 0
R = n-1
L = R
```

For large values, test overflow boundaries.

---

# 54. JAVA-SPECIFIC DSA NOTES

## `Math.max`

```java
currentSum = Math.max(nums[i], currentSum + nums[i]);
```

## `Integer.MIN_VALUE`

Useful for maximum initialization when appropriate:

```java
int max = Integer.MIN_VALUE;
```

## `long`

Use:

```java
long
```

when sums can exceed `int`.

---

# 55. 🎤 INTERVIEW EXPLANATION — PREFIX SUM

> "I use Prefix Sum when there are repeated range-sum calculations. I preprocess the array in O(n), where `prefix[i]` represents the sum of the first `i` elements. Then the inclusive range sum from L to R is `prefix[R+1] - prefix[L]`, which takes O(1). This avoids repeatedly traversing overlapping ranges."

---

# 56. 🎤 INTERVIEW EXPLANATION — KADANE

> "Kadane's Algorithm solves the maximum subarray sum problem in O(n) time and O(1) extra space. At every index, I maintain the best sum of a subarray ending at that index. I either extend the previous subarray or start a new one with the current element, then update the global maximum."

---

# 57. 🧠 PATTERN DECISION TREE

```text
ARRAY / SUBARRAY
       |
       +-- Repeated range sums?
       |       ↓
       |   Prefix Sum
       |
       +-- Maximum contiguous sum?
       |       ↓
       |     Kadane
       |
       +-- Exactly k consecutive elements?
       |       ↓
       |  Sliding Window
       |
       +-- Sum exactly K?
               ↓
       Prefix Sum + HashMap
       (depending on constraints)
```

---

# 58. 📊 COMPLEXITY CHEAT SHEET

| Task | Time | Extra Space |
|---|---:|---:|
| Count subarrays | `O(1)` | `O(1)` |
| Generate all subarrays | `O(n²)` | Depends |
| Triple-loop subarray sums | `O(n³)` | `O(1)` |
| Nested loops + running sum | `O(n²)` | `O(1)` |
| Build Prefix Sum | `O(n)` | `O(n)` |
| One Prefix Sum query | `O(1)` | `O(n)` structure |
| `q` Prefix Sum queries | `O(q)` after build | `O(n)` |
| Kadane | `O(n)` | `O(1)` |
| Kadane + indices | `O(n)` | `O(1)` |

---

# 59. 🧠 30-SECOND REVISION

## Subarray

```text
CONTIGUOUS
```

## Count

```text
n(n+1)/2
```

## Prefix Sum

```java
prefix[0] = 0;

for (int i = 0; i < n; i++) {
    prefix[i + 1] = prefix[i] + nums[i];
}
```

Range:

```java
prefix[right + 1] - prefix[left]
```

Complexity:

```text
Build → O(n)
Query → O(1)
```

## Kadane

```java
currentSum = Math.max(
    nums[i],
    currentSum + nums[i]
);

maxSum = Math.max(maxSum, currentSum);
```

Complexity:

```text
O(n) time
O(1) space
```

Core question:

```text
CONTINUE or RESTART?
```

---

# 60. 🧠 MEMORY TRICKS

### Prefix Sum

Think:

> **"Add everything once, subtract what I don't need."**

```text
prefix[R+1] - prefix[L]
```

### Kadane

Think:

> **"Carry the previous sum or start fresh?"**

```text
max(current,
    previous + current)
```

### Subarray

Think:

> **CONTIGUOUS**

---

# 61. 📝 DAILY QUIZ — 10 QUESTIONS

## Q1

A subarray must be:

A. Sorted  
B. Contiguous  
C. Unique  
D. Positive

## Q2

How many subarrays does an array of length `5` have?

A. `10`  
B. `15`  
C. `20`  
D. `25`

## Q3

Complexity of building Prefix Sum?

A. `O(1)`  
B. `O(log n)`  
C. `O(n)`  
D. `O(n²)`

## Q4

Prefix array for:

```text
[2,4,1,5,3]
```

using the leading-zero convention?

## Q5

For inclusive `[L,R]`, the range sum is:

A. `prefix[R] - prefix[L]`  
B. `prefix[R+1] - prefix[L]`  
C. `prefix[R] + prefix[L]`  
D. `prefix[L] - prefix[R+1]`

## Q6

Kadane's Algorithm primarily solves:

A. Sorting  
B. Maximum contiguous subarray sum  
C. Graph traversal  
D. String matching

## Q7

Why can this be wrong?

```java
int currentSum = 0;
int maxSum = 0;
```

## Q8

Time complexity of Kadane?

A. `O(n³)`  
B. `O(n²)`  
C. `O(n log n)`  
D. `O(n)`

## Q9

For many range-sum queries, which pattern should you consider?

A. Prefix Sum  
B. DFS  
C. Stack  
D. Recursion

## Q10

What does `currentSum` represent?

A. Sum of the whole array  
B. Best subarray sum ending at the current index  
C. Number of negative elements  
D. Prefix sum

---

# 62. 📝 ANSWER KEY

### Q1

**B — Contiguous**

### Q2

**B — 15**

```text
5 × 6 / 2 = 15
```

### Q3

**C — O(n)**

### Q4

```text
[0,2,6,7,12,15]
```

### Q5

**B — `prefix[R+1] - prefix[L]`**

### Q6

**B — Maximum contiguous subarray sum**

### Q7

It can return `0` for an all-negative array, even though the standard problem requires a non-empty subarray.

### Q8

**D — O(n)**

### Q9

**A — Prefix Sum**

### Q10

**B — Best subarray sum ending at the current index**

---

# 63. 🧪 PATTERN RECOGNITION TEST

Classify each problem before coding.

### 1.

> 50,000 queries ask for sum from `L` to `R`.

**Think:** Prefix Sum.

### 2.

> Find the largest sum of a contiguous subarray.

**Think:** Kadane.

### 3.

> Find the maximum sum of exactly `k` consecutive elements.

**Think:** Sliding Window.

### 4.

> Find whether a subarray has sum exactly `K`.

**Think:** Prefix Sum + HashMap may be appropriate.

### 5.

> Find the sum of one specific range.

**Think:** Direct scan is possible; Prefix Sum is useful when many queries exist.

### 6.

> Enumerate every subarray.

**Think:** Nested loops.

---

# 64. 🏆 DAY 4 MASTER CHECKLIST

- [ ] I know what a subarray is.
- [ ] I know what contiguous means.
- [ ] I can distinguish subarray from subsequence.
- [ ] I know `n(n+1)/2`.
- [ ] I can generate all subarrays.
- [ ] I understand why naive subarray processing can be slow.
- [ ] I understand Prefix Sum.
- [ ] I can build a Prefix Sum array.
- [ ] I know why the leading zero is useful.
- [ ] I can calculate `sum(L,R)`.
- [ ] I understand `O(1)` range queries.
- [ ] I know when to use `long`.
- [ ] I understand `currentSum` in Kadane.
- [ ] I understand `maxSum` in Kadane.
- [ ] I can handle all-negative arrays.
- [ ] I understand "continue vs restart."
- [ ] I can compare Prefix Sum and Kadane.
- [ ] I can recognize when Sliding Window may be better.
- [ ] I solved the mini problems.
- [ ] I attempted the practice problems.
- [ ] I completed the quiz.

---

# 65. 🏠 HOMEWORK

## Must Solve

### Prefix Sum

1. Build Prefix Sum manually.
2. Answer 5 range-sum queries.
3. Implement a reusable range-sum class.
4. Solve **Range Sum Query — Immutable**.

### Subarrays

5. Generate every subarray of `[1,2,3]`.
6. Calculate the number of subarrays for `n = 10`.
7. Calculate every subarray sum using nested loops.

### Kadane

8. Implement Kadane from memory.
9. Test:
   ```text
   [1,2,3,4]
   ```
10. Test:
   ```text
   [-5,-2,-8]
   ```
11. Test:
   ```text
   [-2,1,-3,4,-1,2,1,-5,4]
   ```
12. Modify Kadane to return the best start and end indices.

---

# 66. 📚 PRACTICE PROBLEMS

## 🟢 Easy

### 1. Running Sum of 1d Array

**Platform:** LeetCode  
**Pattern:** Running Prefix Sum  
**Expected Complexity:** `O(n)` time

https://leetcode.com/problems/running-sum-of-1d-array/

### 2. Range Sum Query — Immutable

**Platform:** LeetCode  
**Difficulty:** Easy  
**Pattern:** Prefix Sum  
**Why:** Direct practice of preprocessing and constant-time range queries.  
**Expected Complexity:** `O(n)` preprocessing, `O(1)` query

https://leetcode.com/problems/range-sum-query-immutable/

---

## 🟡 Medium

### 3. Maximum Subarray

**Platform:** LeetCode  
**Difficulty:** Medium  
**Pattern:** Kadane  
**Why:** Canonical maximum-subarray problem.  
**Expected Complexity:** `O(n)` time, `O(1)` extra space

https://leetcode.com/problems/maximum-subarray/

### 4. Subarray Sum Equals K

**Platform:** LeetCode  
**Difficulty:** Medium  
**Pattern:** Prefix Sum + HashMap  
**Why:** Extends Prefix Sum into a frequency-based problem.  
**What to notice:** Two prefix sums whose difference is `K` identify a qualifying subarray.  
**Expected Complexity:** `O(n)` time, `O(n)` space

https://leetcode.com/problems/subarray-sum-equals-k/

### 5. Maximum Size Subarray Sum Equals k

**Platform:** LeetCode  
**Difficulty:** Medium  
**Pattern:** Prefix Sum + HashMap  
**Why:** Shows how Prefix Sum can identify a longest qualifying subarray.  
**Expected Complexity:** `O(n)` time, `O(n)` space

https://leetcode.com/problems/maximum-size-subarray-sum-equals-k/

---

## 🟢 HackerRank

### 6. The Maximum Subarray

**Platform:** HackerRank  
**Pattern:** Maximum subarray / Kadane  
**Why:** Useful for practicing contiguous and non-contiguous variants.

https://www.hackerrank.com/challenges/maxsubarray/problem

---

# 67. PRACTICE ORDER

```text
1. Running Sum of 1d Array
        ↓
2. Range Sum Query — Immutable
        ↓
3. Maximum Subarray
        ↓
4. The Maximum Subarray
        ↓
5. Subarray Sum Equals K
        ↓
6. Maximum Size Subarray Sum Equals k
```

First become fluent with:

```text
Prefix Sum
+
Kadane
```

Then move to Prefix Sum + HashMap.

---

# 68. 🎯 FINAL DAY 4 MINDSET

When you see a subarray problem:

```text
Is it CONTIGUOUS?
        ↓
What exactly is being asked?
        ↓
Repeated range sums?
        → Prefix Sum

Maximum contiguous sum?
        → Kadane

Fixed-size consecutive range?
        → Sliding Window

Exact target sum?
        → Prefix Sum + HashMap may help
```

The real lesson is:

> **Reduce repeated work by identifying exactly what information needs to be carried forward or precomputed.**

---

# 69. 🔗 NAVIGATION

⬅️ [Day 3 — Arrays Fundamentals](Day-03-Arrays-Fundamentals.md)

➡️ [Day 5 — Strings + Hashing](Day-05-Strings-Hashing.md)

---

**End of Day 4**
