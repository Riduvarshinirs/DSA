# 🔥 DAY 6 --- TWO POINTERS + SLIDING WINDOW

## Today's Goal

Today you will learn two of the most important placement problem-solving
patterns:

> **Two Pointers**

> **Sliding Window**

By the end of today, you should be able to look at a problem and
recognize:

-   When two pointers can replace nested loops
-   When a sorted array allows an `O(n)` pair-search
-   How `left` and `right` pointers move
-   How the slow/fast pointer idea works
-   How to remove duplicates in-place
-   How to move elements while preserving relative order
-   How a fixed-size sliding window works
-   How a variable-size sliding window works
-   How to expand and shrink a window
-   How to maintain a sum, count, or frequency inside a window
-   How to convert brute force solutions into `O(n)` solutions
-   When two pointers and sliding window should **not** be used

------------------------------------------------------------------------

# 1. PREREQUISITES

You should already know:

-   Java basics
-   `for` and `while` loops
-   Arrays
-   Strings
-   `HashMap`
-   `HashSet`
-   Basic time and space complexity
-   Subarrays and substrings
-   Basic frequency counting

These were covered in the previous days.

> **Important:** This file does not reteach Java basics, arrays,
> strings, or hashing from scratch. It builds on them.

------------------------------------------------------------------------

# 2. PRIORITY

  Topic                       Priority
  --------------------------- ------------
  Two Pointers                🔥🔥🔥🔥🔥
  Pair Sum in Sorted Array    🔥🔥🔥🔥🔥
  Remove Duplicates           🔥🔥🔥🔥
  Move Zeroes                 🔥🔥🔥🔥
  Fixed Sliding Window        🔥🔥🔥🔥🔥
  Variable Sliding Window     🔥🔥🔥🔥🔥
  Longest Valid Window        🔥🔥🔥🔥🔥
  Minimum Valid Window        🔥🔥🔥🔥
  Container With Most Water   🔥🔥🔥🔥
  3Sum                        🔥🔥🔥🔥
  Pattern Recognition         🔥🔥🔥🔥🔥

------------------------------------------------------------------------

# 3. THE BIG IDEA

There is one question you should keep asking:

> **"Am I repeatedly checking overlapping elements?"**

If yes, there may be a way to avoid recomputing them.

Two pointers and sliding window are techniques for **reusing work**.

Instead of:

``` text
Check everything again
Check everything again
Check everything again
...
```

we try:

``` text
Move a pointer
Reuse what we already know
Move another pointer
Continue
```

This is why many `O(n²)` solutions can become `O(n)`.

------------------------------------------------------------------------

# 4. TWO POINTERS

## 🧑‍🎓 Beginner Explanation

Two pointers means:

> Use two indexes to explore an array/string instead of repeatedly
> starting from the beginning.

The two pointers are often named:

``` java
left
right
```

Example:

``` text
index:  0   1   2   3   4
        ↓           ↓
      left        right
```

The pointers may:

-   move toward each other
-   move in the same direction
-   move at different speeds
-   represent the beginning/end of a useful region

------------------------------------------------------------------------

## Why Do We Need Two Pointers?

Suppose:

``` text
[1, 2, 3, 4, 5]
```

You want to find two numbers whose sum is `6`.

Brute force:

``` text
1 + 2
1 + 3
1 + 4
1 + 5
2 + 3
2 + 4
...
```

This is `O(n²)`.

But because the array is sorted, we can use:

``` text
left = 0
right = n - 1
```

Then intelligently move one pointer.

This gives:

``` text
O(n)
```

------------------------------------------------------------------------

# 5. TWO POINTER TYPES

There are two major forms you should recognize.

## Type 1 --- Opposite Direction

Pointers start at opposite ends:

``` text
left →             ← right
[1, 2, 3, 4, 5, 6]
```

They move toward each other.

Common problems:

-   Pair sum in sorted array
-   Container With Most Water
-   Palindrome checking
-   Some partitioning problems

------------------------------------------------------------------------

## Type 2 --- Same Direction

Both pointers move from left to right:

``` text
slow →
fast →
[1, 1, 2, 2, 3, 4]
```

Common problems:

-   Remove duplicates
-   Move zeroes
-   Slow/fast pointer patterns
-   In-place array transformations

------------------------------------------------------------------------

# 6. OPPOSITE-DIRECTION TWO POINTERS

## The Core Rule

For a sorted array:

``` text
if current sum < target:
    move left forward

if current sum > target:
    move right backward

if current sum == target:
    answer found
```

Why?

Because the array is sorted.

If:

``` text
arr[left] + arr[right] < target
```

then keeping the same `left` and moving `right` left would only make the
sum smaller.

So we need a larger value.

Therefore:

``` text
left++
```

Similarly, if the sum is too large:

``` text
right--
```

------------------------------------------------------------------------

# 7. VISUALIZATION --- PAIR SUM

Array:

``` text
[1, 2, 3, 4, 6, 8]
```

Target:

``` text
10
```

Start:

``` text
L               R
↓               ↓
1  2  3  4  6  8
```

Sum:

``` text
1 + 8 = 9
```

Too small.

Move `L`:

``` text
   L            R
   ↓            ↓
1  2  3  4  6  8
```

Now:

``` text
2 + 8 = 10
```

Found.

------------------------------------------------------------------------

# 8. JAVA TEMPLATE --- OPPOSITE POINTERS

``` java
int left = 0;
int right = arr.length - 1;

while (left < right) {

    int sum = arr[left] + arr[right];

    if (sum == target) {
        // answer
        break;
    } 
    else if (sum < target) {
        left++;
    } 
    else {
        right--;
    }
}
```

### 30-Second Revision

``` text
Sorted + pair target
        ↓
left + right
        ↓
sum < target → left++
sum > target → right--
sum == target → found
```

------------------------------------------------------------------------

# 9. EXAMPLE 1 --- VERY EASY

## Problem

Given a sorted array, determine whether two numbers add up to the
target.

### Input

``` text
arr = [1, 2, 4, 6, 8, 9]
target = 10
```

------------------------------------------------------------------------

## Observation

Start with:

``` text
1 + 9 = 10
```

So the answer is immediately true.

------------------------------------------------------------------------

## Approach

Use two pointers.

``` text
left = 0
right = n - 1
```

------------------------------------------------------------------------

## Algorithm

1.  Set `left = 0`
2.  Set `right = n - 1`
3.  Calculate the sum
4.  If sum equals target, return true
5.  If sum is smaller, increment `left`
6.  If sum is larger, decrement `right`
7.  Continue while `left < right`

------------------------------------------------------------------------

## Code

``` java
public static boolean hasPair(int[] arr, int target) {

    int left = 0;
    int right = arr.length - 1;

    while (left < right) {

        int sum = arr[left] + arr[right];

        if (sum == target) {
            return true;
        } else if (sum < target) {
            left++;
        } else {
            right--;
        }
    }

    return false;
}
```

------------------------------------------------------------------------

## Complexity

``` text
Time:  O(n)
Space: O(1)
```

------------------------------------------------------------------------

# 10. BRUTE FORCE → TWO POINTERS

## Brute Force

``` java
for (int i = 0; i < n; i++) {
    for (int j = i + 1; j < n; j++) {
        if (arr[i] + arr[j] == target) {
            return true;
        }
    }
}
```

Complexity:

``` text
O(n²)
```

------------------------------------------------------------------------

## Bottleneck

We examine many pairs.

------------------------------------------------------------------------

## Observation

The array is sorted.

Therefore, we know how the sum changes when moving either end.

------------------------------------------------------------------------

## Pattern

``` text
Sorted array + pair condition
            ↓
       Two pointers
```

------------------------------------------------------------------------

## Optimal

``` text
O(n)
```

This is a major placement pattern.

------------------------------------------------------------------------

# 11. IMPORTANT CONDITION

Two-pointer pair sum does **not** automatically work on an arbitrary
unsorted array.

Example:

``` text
[8, 1, 6, 3]
```

The relationship between moving `left` or `right` and changing the sum
is not predictable.

You can:

1.  Sort the array first, or
2.  Use a HashSet/HashMap approach depending on the required output.

Sorting changes the complexity:

``` text
Sort: O(n log n)
Two pointers: O(n)

Overall: O(n log n)
```

------------------------------------------------------------------------

# 12. SAME-DIRECTION TWO POINTERS

Now the pointers move in the same direction.

Example:

``` text
slow
 ↓
[1, 1, 2, 2, 3]
 ↑
fast
```

The idea is:

> One pointer represents the position where the next useful element
> should go.

The other pointer scans the input.

This is extremely useful for **in-place array modification**.

------------------------------------------------------------------------

# 13. REMOVE DUPLICATES FROM SORTED ARRAY

## Problem

Given a sorted array, remove duplicates in-place so that each value
appears only once.

Example:

``` text
[1, 1, 2, 2, 3]
```

After processing:

``` text
[1, 2, 3, ...]
```

The important point:

> We usually do not physically shrink the Java array.

Instead, we overwrite the beginning of the array.

Return the number of unique elements.

------------------------------------------------------------------------

# 14. VISUALIZATION

Input:

``` text
[1, 1, 2, 2, 3]
```

Think:

``` text
slow = position of last unique element
fast = scanner
```

Initially:

``` text
slow
 ↓
[1, 1, 2, 2, 3]
 ↓
fast
```

When:

``` text
arr[fast] != arr[slow]
```

we found a new unique value.

Move `slow` and copy it.

------------------------------------------------------------------------

# 15. JAVA CODE

``` java
public static int removeDuplicates(int[] nums) {

    if (nums.length == 0) {
        return 0;
    }

    int slow = 0;

    for (int fast = 1; fast < nums.length; fast++) {

        if (nums[fast] != nums[slow]) {
            slow++;
            nums[slow] = nums[fast];
        }
    }

    return slow + 1;
}
```

------------------------------------------------------------------------

## Dry Run

``` text
nums = [1, 1, 2, 2, 3]
```

Start:

``` text
slow = 0
```

### fast = 1

``` text
nums[1] == nums[0]
```

Duplicate.

Do nothing.

### fast = 2

``` text
2 != 1
```

Move:

``` text
slow = 1
nums[1] = 2
```

Array becomes:

``` text
[1, 2, 2, 2, 3]
```

### fast = 3

Duplicate.

### fast = 4

``` text
3 != 2
```

Move:

``` text
slow = 2
nums[2] = 3
```

Result:

``` text
[1, 2, 3, 2, 3]
```

Valid portion:

``` text
[1, 2, 3]
```

Return:

``` text
3
```

------------------------------------------------------------------------

## Complexity

``` text
Time:  O(n)
Space: O(1)
```

------------------------------------------------------------------------

# 16. MOVE ZEROES

## Problem

Move all zeroes to the end while keeping the relative order of non-zero
elements.

Example:

``` text
Input:
[0, 1, 0, 3, 12]

Output:
[1, 3, 12, 0, 0]
```

------------------------------------------------------------------------

# 17. IDEA

Use a pointer:

``` text
insertPos
```

It represents:

> Where should the next non-zero element be placed?

Scan with another pointer.

Whenever we find a non-zero:

``` text
nums[insertPos] = nums[i]
insertPos++
```

Then fill the remaining positions with zero.

------------------------------------------------------------------------

# 18. JAVA CODE

``` java
public static void moveZeroes(int[] nums) {

    int insertPos = 0;

    for (int i = 0; i < nums.length; i++) {

        if (nums[i] != 0) {
            nums[insertPos] = nums[i];
            insertPos++;
        }
    }

    while (insertPos < nums.length) {
        nums[insertPos] = 0;
        insertPos++;
    }
}
```

------------------------------------------------------------------------

## Complexity

``` text
Time:  O(n)
Space: O(1)
```

------------------------------------------------------------------------

# 19. TWO POINTER PATTERN MAP

  Problem clue             Pattern
  ------------------------ -------------------------
  Sorted + pair target     Opposite pointers
  Compare from both ends   Opposite pointers
  Palindrome               Opposite pointers
  In-place filtering       Same-direction pointers
  Remove duplicates        Slow/Fast
  Move elements            Slow/Fast
  Need to preserve order   Often slow/fast

------------------------------------------------------------------------

# 20. VALID PALINDROME

A palindrome reads the same forward and backward.

Examples:

``` text
madam → palindrome
racecar → palindrome
hello → not palindrome
```

If the problem asks to ignore:

-   spaces
-   punctuation
-   capitalization

then preprocessing or character checks are needed.

------------------------------------------------------------------------

## Two Pointer Idea

``` text
left →       ← right
r a c e c a r
```

Compare:

``` text
s[left]
s[right]
```

If they differ:

``` text
return false
```

Otherwise:

``` text
left++
right--
```

------------------------------------------------------------------------

## Java Code

``` java
public static boolean isPalindrome(String s) {

    int left = 0;
    int right = s.length() - 1;

    while (left < right) {

        while (left < right && !Character.isLetterOrDigit(s.charAt(left))) {
            left++;
        }

        while (left < right && !Character.isLetterOrDigit(s.charAt(right))) {
            right--;
        }

        if (Character.toLowerCase(s.charAt(left)) !=
            Character.toLowerCase(s.charAt(right))) {
            return false;
        }

        left++;
        right--;
    }

    return true;
}
```

------------------------------------------------------------------------

## Complexity

``` text
Time:  O(n)
Space: O(1)
```

------------------------------------------------------------------------

# 21. SLIDING WINDOW

Now we move to another extremely important pattern.

## 🧑‍🎓 Beginner Explanation

A sliding window is a special way of using two pointers to represent a
**contiguous portion** of an array or string.

Example:

``` text
[2, 5, 1, 8, 3, 4]
```

A window might be:

``` text
[2, 5, 1]
```

Then slide:

``` text
    [5, 1, 8]
```

Then:

``` text
       [1, 8, 3]
```

Then:

``` text
          [8, 3, 4]
```

Instead of recalculating every window from scratch, we update the
existing window.

------------------------------------------------------------------------

# 22. WHY SLIDING WINDOW?

Suppose:

``` text
arr = [1, 2, 3, 4, 5]
k = 3
```

You want every sum of 3 consecutive elements.

Brute force:

``` text
1 + 2 + 3
2 + 3 + 4
3 + 4 + 5
```

Notice the overlap.

From:

``` text
1 + 2 + 3 = 6
```

to:

``` text
2 + 3 + 4
```

we do not need to calculate everything again.

Remove:

``` text
1
```

Add:

``` text
4
```

So:

``` text
newSum = oldSum - 1 + 4
```

This is the core idea.

------------------------------------------------------------------------

# 23. TYPES OF SLIDING WINDOW

## Type 1 --- Fixed Size

Window size remains constant.

Examples:

``` text
maximum sum of k elements
maximum average of k elements
count windows of size k
```

Template:

``` text
add right
if window size > k:
    remove left
```

------------------------------------------------------------------------

## Type 2 --- Variable Size

Window expands and shrinks depending on a condition.

Examples:

``` text
longest substring without repeating characters
minimum size subarray with sum >= target
longest subarray satisfying a condition
```

Template:

``` text
expand right

while window is invalid:
    shrink left

update answer
```

------------------------------------------------------------------------

# 24. FIXED WINDOW TEMPLATE

``` java
int left = 0;
long window = 0;

for (int right = 0; right < n; right++) {

    window += arr[right];

    if (right - left + 1 > k) {
        window -= arr[left];
        left++;
    }

    if (right - left + 1 == k) {
        // process window
    }
}
```

### 30-Second Revision

``` text
right enters
left exits
window size = k
```

------------------------------------------------------------------------

# 25. EXAMPLE --- MAXIMUM SUM OF K CONSECUTIVE ELEMENTS

## Input

``` text
arr = [2, 1, 5, 1, 3, 2]
k = 3
```

Windows:

``` text
[2,1,5] = 8
[1,5,1] = 7
[5,1,3] = 9
[1,3,2] = 6
```

Answer:

``` text
9
```

------------------------------------------------------------------------

## Brute Force

``` java
int max = Integer.MIN_VALUE;

for (int i = 0; i <= n - k; i++) {

    int sum = 0;

    for (int j = i; j < i + k; j++) {
        sum += arr[j];
    }

    max = Math.max(max, sum);
}
```

Complexity:

``` text
O(nk)
```

------------------------------------------------------------------------

## Bottleneck

The overlapping elements are added repeatedly.

------------------------------------------------------------------------

## Observation

When the window moves one position:

``` text
remove left element
add new right element
```

------------------------------------------------------------------------

## Optimal Code

``` java
public static long maxSum(int[] arr, int k) {

    if (k <= 0 || k > arr.length) {
        throw new IllegalArgumentException("Invalid window size");
    }

    long windowSum = 0;

    for (int i = 0; i < k; i++) {
        windowSum += arr[i];
    }

    long maxSum = windowSum;

    for (int right = k; right < arr.length; right++) {

        windowSum += arr[right];
        windowSum -= arr[right - k];

        maxSum = Math.max(maxSum, windowSum);
    }

    return maxSum;
}
```

------------------------------------------------------------------------

## Complexity

``` text
Time:  O(n)
Space: O(1)
```

------------------------------------------------------------------------

# 26. VARIABLE-SIZE SLIDING WINDOW

This is one of the most important patterns for placements.

The window does not have a fixed size.

It grows until something happens.

General idea:

``` text
right →
```

Expand the window.

Then:

``` text
while invalid:
    left++
```

Once valid:

``` text
update answer
```

------------------------------------------------------------------------

# 27. THE UNIVERSAL VARIABLE WINDOW TEMPLATE

``` java
int left = 0;

for (int right = 0; right < n; right++) {

    // Add arr[right] to the window

    while (/* window is invalid */) {

        // Remove arr[left]

        left++;
    }

    // Window is valid here

    // Update answer
}
```

Memorize this structure.

------------------------------------------------------------------------

# 28. HOW TO THINK ABOUT VARIABLE WINDOWS

Think:

``` text
EXPAND → CHECK → SHRINK → RECORD
```

More precisely:

``` text
right moves →
        ↓
window expands
        ↓
condition becomes invalid
        ↓
left moves →
        ↓
window becomes valid
        ↓
record answer
```

------------------------------------------------------------------------

# 29. MINIMUM SIZE SUBARRAY SUM

## Problem

Given positive integers, find the minimum length of a contiguous
subarray whose sum is at least `target`.

Example:

``` text
target = 7
nums = [2, 3, 1, 2, 4, 3]
```

Possible valid windows:

``` text
[2,3,1,2] = 8 → length 4
[3,1,2,4] = 10 → length 4
[4,3] = 7 → length 2
```

Answer:

``` text
2
```

------------------------------------------------------------------------

# 30. WHY BRUTE FORCE IS SLOW

You could examine every subarray:

``` text
start at every index
extend to every later index
calculate the sum
```

This can be `O(n²)`.

But because all numbers are **positive**, when we expand the window, the
sum increases.

That gives us a useful property.

------------------------------------------------------------------------

# 31. SLIDING WINDOW APPROACH

``` text
right enters → sum increases
left leaves  → sum decreases
```

Whenever:

``` text
sum >= target
```

the current window is valid.

But we want the **smallest** valid window.

Therefore:

``` text
while sum >= target:
    update minimum
    remove left
    left++
```

------------------------------------------------------------------------

# 32. JAVA CODE

``` java
public static int minSubArrayLen(int target, int[] nums) {

    int left = 0;
    long sum = 0;
    int minLength = Integer.MAX_VALUE;

    for (int right = 0; right < nums.length; right++) {

        sum += nums[right];

        while (sum >= target) {

            minLength = Math.min(minLength, right - left + 1);

            sum -= nums[left];
            left++;
        }
    }

    return minLength == Integer.MAX_VALUE ? 0 : minLength;
}
```

------------------------------------------------------------------------

## Dry Run

``` text
target = 7
[2,3,1,2,4,3]
```

Start:

``` text
left = 0
sum = 0
```

Add `2`:

``` text
sum = 2
```

Add `3`:

``` text
sum = 5
```

Add `1`:

``` text
sum = 6
```

Add `2`:

``` text
sum = 8
```

Valid.

Window:

``` text
[2,3,1,2]
```

Length:

``` text
4
```

Shrink:

``` text
remove 2
sum = 6
```

Continue.

Eventually:

``` text
[4,3]
```

Sum:

``` text
7
```

Length:

``` text
2
```

Answer:

``` text
2
```

------------------------------------------------------------------------

## Complexity

``` text
Time:  O(n)
Space: O(1)
```

Why `O(n)` even though there is a `while` loop?

Because `left` only moves forward.

Across the entire algorithm:

``` text
right moves at most n times
left moves at most n times
```

Therefore:

``` text
O(n + n) = O(n)
```

------------------------------------------------------------------------

# 33. IMPORTANT SLIDING WINDOW CONDITION

The previous minimum-size example relies on positive numbers.

Why?

Because:

``` text
add positive → sum increases
remove positive → sum decreases
```

This predictable behavior makes shrinking meaningful.

If negative values are allowed, this simple sliding-window logic may no
longer work.

This is a critical interview point.

------------------------------------------------------------------------

# 34. LONGEST SUBSTRING WITHOUT REPEATING CHARACTERS

You saw this problem in the Strings + Hashing day.

Today we focus on the **sliding-window pattern** behind it.

Example:

``` text
abcabcbb
```

Longest substring without repeated characters:

``` text
abc
```

Length:

``` text
3
```

------------------------------------------------------------------------

# 35. WINDOW IDEA

Maintain:

``` text
[left ... right]
```

such that:

> The current window contains no duplicate characters.

Expand `right`.

If the new character creates a duplicate:

``` text
shrink from left
```

until the window becomes valid again.

------------------------------------------------------------------------

# 36. JAVA CODE --- HASHSET VERSION

``` java
public static int lengthOfLongestSubstring(String s) {

    HashSet<Character> set = new HashSet<>();

    int left = 0;
    int maxLength = 0;

    for (int right = 0; right < s.length(); right++) {

        char ch = s.charAt(right);

        while (set.contains(ch)) {
            set.remove(s.charAt(left));
            left++;
        }

        set.add(ch);

        maxLength = Math.max(maxLength, right - left + 1);
    }

    return maxLength;
}
```

------------------------------------------------------------------------

## Complexity

``` text
Time:  O(n)
Space: O(k)
```

where `k` is the number of distinct characters in the window/alphabet.

------------------------------------------------------------------------

# 37. WHY THIS IS SLIDING WINDOW

The key is not the `HashSet`.

The key is:

``` text
[left ... right]
```

The set is only helping us maintain a property:

``` text
No duplicate characters
```

Pattern:

``` text
Expand right
     ↓
Duplicate?
     ↓ yes
Shrink left
     ↓
Valid window
     ↓
Update maximum
```

------------------------------------------------------------------------

# 38. FIXED VS VARIABLE WINDOW

  Feature         Fixed Window             Variable Window
  --------------- ------------------------ ---------------------------
  Size            Constant                 Changes
  Example         max sum of k             longest valid substring
  Right pointer   Expands                  Expands
  Left pointer    Moves to maintain size   Moves to restore validity
  Main question   Exactly k?               Longest/shortest valid?

------------------------------------------------------------------------

# 39. TWO POINTERS VS SLIDING WINDOW

They overlap, but they are not exactly the same concept.

### Two Pointers

General technique using two indexes.

``` text
left
right
```

They may represent:

-   two independent positions
-   opposite ends
-   slow/fast positions

### Sliding Window

A specific use of two pointers where:

``` text
[left ... right]
```

represents a contiguous region.

Think:

``` text
Two pointers
    ↓
broader technique

Sliding window
    ↓
two pointers representing a window
```

------------------------------------------------------------------------

# 40. CONTAINER WITH MOST WATER

## Problem

Given heights:

``` text
[1,8,6,2,5,4,8,3,7]
```

Choose two vertical lines that contain the maximum amount of water.

Formula:

``` text
area = min(height[left], height[right])
       × (right - left)
```

------------------------------------------------------------------------

# 41. BRUTE FORCE

Try every pair:

``` java
for (int i = 0; i < n; i++) {
    for (int j = i + 1; j < n; j++) {

        int width = j - i;
        int height = Math.min(height[i], height[j]);

        max = Math.max(max, width * height);
    }
}
```

Complexity:

``` text
O(n²)
```

------------------------------------------------------------------------

# 42. TWO POINTER OBSERVATION

Start:

``` text
left = 0
right = n - 1
```

The width is largest initially.

The area is limited by the shorter line.

Therefore, moving the taller line inward cannot increase the limiting
height.

So:

> Move the pointer at the shorter height.

This is the critical insight.

------------------------------------------------------------------------

# 43. JAVA CODE

``` java
public static int maxArea(int[] height) {

    int left = 0;
    int right = height.length - 1;

    int maxArea = 0;

    while (left < right) {

        int width = right - left;
        int currentHeight = Math.min(height[left], height[right]);

        int area = width * currentHeight;

        maxArea = Math.max(maxArea, area);

        if (height[left] < height[right]) {
            left++;
        } else {
            right--;
        }
    }

    return maxArea;
}
```

------------------------------------------------------------------------

## Complexity

``` text
Time:  O(n)
Space: O(1)
```

------------------------------------------------------------------------

# 44. 3SUM --- TWO POINTER EXTENSION

This is a more advanced use of two pointers.

## Problem

Find all unique triplets whose sum is zero.

Example:

``` text
[-1, 0, 1, 2, -1, -4]
```

Output:

``` text
[-1, -1, 2]
[-1, 0, 1]
```

------------------------------------------------------------------------

# 45. MAIN IDEA

First sort:

``` text
[-4, -1, -1, 0, 1, 2]
```

Fix one number:

``` text
i
```

Then solve a two-sum problem on the remaining suffix using:

``` text
left
right
```

So:

``` text
3Sum
  ↓
Fix one number
  ↓
Two pointers for remaining two numbers
```

------------------------------------------------------------------------

# 46. JAVA CODE

``` java
import java.util.*;

public static List<List<Integer>> threeSum(int[] nums) {

    List<List<Integer>> result = new ArrayList<>();

    Arrays.sort(nums);

    for (int i = 0; i < nums.length - 2; i++) {

        if (i > 0 && nums[i] == nums[i - 1]) {
            continue;
        }

        int left = i + 1;
        int right = nums.length - 1;

        while (left < right) {

            long sum = (long) nums[i] + nums[left] + nums[right];

            if (sum == 0) {

                result.add(Arrays.asList(
                    nums[i],
                    nums[left],
                    nums[right]
                ));

                left++;
                right--;

                while (left < right && nums[left] == nums[left - 1]) {
                    left++;
                }

                while (left < right && nums[right] == nums[right + 1]) {
                    right--;
                }

            } else if (sum < 0) {
                left++;
            } else {
                right--;
            }
        }
    }

    return result;
}
```

------------------------------------------------------------------------

## Complexity

Sorting:

``` text
O(n log n)
```

Outer loop + two pointers:

``` text
O(n²)
```

Overall:

``` text
O(n²)
```

Space depends on the required output; excluding output, the algorithm
uses constant auxiliary space apart from the sorting implementation.

------------------------------------------------------------------------

# 47. WHY SORTING HELPS AGAIN

Sorting creates order.

Order allows us to reason:

``` text
sum too small → move left
sum too large → move right
```

This is why sorting appears frequently before two-pointer solutions.

------------------------------------------------------------------------

# 48. BRUTE FORCE → OPTIMAL PATTERN

## Pattern 1 --- Pair Sum

``` text
Nested loops
O(n²)
   ↓
sorted array
   ↓
two pointers
O(n)
```

------------------------------------------------------------------------

## Pattern 2 --- Fixed Window

``` text
Recalculate every k elements
O(nk)
   ↓
reuse previous sum
   ↓
sliding window
O(n)
```

------------------------------------------------------------------------

## Pattern 3 --- Longest Valid Window

``` text
Try every substring
O(n²) or worse
   ↓
maintain validity
   ↓
expand + shrink
O(n)
```

------------------------------------------------------------------------

# 49. PATTERN RECOGNITION

When you see:

### Clue 1

> "The array is sorted and find a pair..."

Think:

``` text
Two pointers
```

------------------------------------------------------------------------

### Clue 2

> "Two numbers whose sum is target"

Ask:

``` text
Is the array sorted?
```

If yes:

``` text
Two pointers
```

If no:

``` text
HashMap/HashSet
```

may be appropriate.

------------------------------------------------------------------------

### Clue 3

> "Exactly k consecutive elements"

Think:

``` text
Fixed sliding window
```

------------------------------------------------------------------------

### Clue 4

> "Maximum sum of k consecutive..."

Think:

``` text
Fixed sliding window
```

------------------------------------------------------------------------

### Clue 5

> "Longest substring/subarray satisfying..."

Think:

``` text
Variable sliding window
```

------------------------------------------------------------------------

### Clue 6

> "Minimum length subarray whose sum is at least..."

For positive numbers:

``` text
Variable sliding window
```

------------------------------------------------------------------------

### Clue 7

> "Expand until invalid, then shrink..."

Think:

``` text
Variable sliding window
```

------------------------------------------------------------------------

### Clue 8

> "In-place remove/filter elements"

Think:

``` text
Slow + fast pointers
```

------------------------------------------------------------------------

# 50. THE MOST IMPORTANT WINDOW QUESTION

Whenever you see:

``` text
subarray
substring
contiguous
consecutive
longest
shortest
at most k
exactly k
```

ask:

> **Can I maintain a window instead of starting over for every
> segment?**

This question will help you recognize many sliding-window problems.

------------------------------------------------------------------------

# 51. COMMON BEGINNER MISTAKES

## Mistake 1 --- Using two pointers on an unsorted array

Incorrect assumption:

> Two pointers always work for pair sum.

They do not.

The movement rule depends on useful ordering or another invariant.

------------------------------------------------------------------------

## Mistake 2 --- Moving the wrong pointer

For sorted pair sum:

``` text
sum < target → left++
sum > target → right--
```

Do not randomly move either pointer.

------------------------------------------------------------------------

## Mistake 3 --- Forgetting `left < right`

For opposite pointers:

``` java
while (left < right)
```

is usually the correct boundary.

------------------------------------------------------------------------

## Mistake 4 --- Recalculating the entire window

Wrong:

``` text
for every window:
    calculate complete sum again
```

Better:

``` text
remove outgoing element
add incoming element
```

------------------------------------------------------------------------

## Mistake 5 --- Updating answer at the wrong time

For a **longest valid** window:

``` text
restore validity
then update max
```

For a **minimum valid** window:

``` text
while valid:
    update min
    shrink
```

------------------------------------------------------------------------

## Mistake 6 --- Using `if` instead of `while` when repeated shrinking is needed

Example:

``` java
while (sum >= target) {
    ...
}
```

may need multiple left moves.

Using only:

``` java
if (sum >= target)
```

can miss smaller valid windows.

------------------------------------------------------------------------

## Mistake 7 --- Forgetting that a window is contiguous

Sliding window works on:

``` text
[left ... right]
```

which is contiguous.

It does not directly solve arbitrary subsequence problems.

------------------------------------------------------------------------

## Mistake 8 --- Integer overflow

If values can be large:

``` java
long sum
```

may be safer than:

``` java
int sum
```

------------------------------------------------------------------------

# 52. EDGE CASES

Always test:

### Empty array

``` text
[]
```

### One element

``` text
[5]
```

### Window size 1

``` text
k = 1
```

### Window size equals array length

``` text
k = n
```

### Window size greater than array length

Handle according to the problem specification.

### All elements equal

``` text
[5,5,5,5]
```

### All zeroes

``` text
[0,0,0]
```

### Negative values

Do not blindly use positive-number sliding-window logic.

### Duplicate-heavy strings

``` text
aaaaaa
```

### No valid window

Return the value required by the problem, often:

``` text
0
```

or:

``` text
-1
```

depending on the specification.

------------------------------------------------------------------------

# 53. JAVA-SPECIFIC DSA NOTES

## `Math.min`

``` java
int x = Math.min(a, b);
```

## `Math.max`

``` java
int x = Math.max(a, b);
```

## Character checks

``` java
Character.isLetterOrDigit(ch)
Character.toLowerCase(ch)
```

## Array sorting

``` java
Arrays.sort(arr);
```

Remember:

``` text
Sorting modifies the array.
```

------------------------------------------------------------------------

# 54. INTERVIEW EXPLANATION --- TWO POINTERS

If interviewer asks:

> Why did you use two pointers?

Say:

> "The problem has a structure that allows me to maintain two indexes
> instead of checking every pair. Since the array is sorted, the sum
> gives directional information. If the sum is smaller than the target,
> I move the left pointer to increase it; if the sum is larger, I move
> the right pointer to decrease it. Each pointer moves at most n times,
> giving O(n) time and O(1) extra space."

------------------------------------------------------------------------

# 55. INTERVIEW EXPLANATION --- SLIDING WINDOW

If interviewer asks:

> Why sliding window?

Say:

> "The problem deals with a contiguous subarray or substring, and
> consecutive windows overlap heavily. Instead of recomputing every
> window, I maintain a window using left and right pointers. The right
> pointer expands the window, and the left pointer removes elements
> whenever the window violates the required condition. Since each
> pointer moves forward at most n times, the overall complexity is
> O(n)."

------------------------------------------------------------------------

# 56. INTERVIEW EXPLANATION --- FIXED WINDOW

> "Because the window size is fixed at k, I maintain the sum of the
> current k elements. When the window moves one position, I subtract the
> element leaving from the left and add the new element entering from
> the right. This reduces the repeated work from O(nk) to O(n)."

------------------------------------------------------------------------

# 57. INTERVIEW EXPLANATION --- VARIABLE WINDOW

> "I maintain a window that satisfies the required condition. I expand
> it using the right pointer and, whenever it becomes invalid, move the
> left pointer until it becomes valid again. I update the answer at the
> point required by whether the problem asks for the longest or shortest
> valid window."

------------------------------------------------------------------------

# 58. CONSTRAINT THINKING

Before coding, look at `n`.

### If:

``` text
n <= 20
```

`O(n²)` may be acceptable.

### If:

``` text
n ≈ 10^5
```

an `O(n²)` solution is usually too slow.

Look for:

``` text
O(n)
O(n log n)
```

Two pointers and sliding window are often ways to reach these
complexities.

------------------------------------------------------------------------

# 59. QUICK DECISION TREE

``` text
Is the problem about pairs?
        |
        |-- Is the array sorted?
        |       |
        |       YES → Two pointers
        |
        NO → Consider HashMap/HashSet
```

For contiguous regions:

``` text
Is it subarray/substring?
        |
        YES
        |
        Is window size fixed?
        |
        |-- YES → Fixed sliding window
        |
        NO
        |
        Is there a validity condition?
        |
        YES → Variable sliding window
```

For in-place filtering:

``` text
Need to preserve useful elements?
        |
        YES
        |
        Slow + Fast pointers
```

------------------------------------------------------------------------

# 60. MINI PRACTICE --- PROBLEM 1

## Move All Negative Numbers to One Side

Given an array, move all negative numbers to the left side and
non-negative numbers to the right side.

Example:

``` text
Input:
[2, -3, 4, -1, 0, -5]

Possible output:
[-3, -1, -5, 2, 4, 0]
```

The exact ordering of the two groups may depend on the problem
specification.

### Hint

Think about:

``` text
left
right
```

and what each pointer should look for.

### What to Notice

This is a partition-style two-pointer problem.

------------------------------------------------------------------------

# 61. MINI PRACTICE --- PROBLEM 2

## Maximum Sum of Exactly K Elements

Given:

``` text
arr = [4, 2, 7, 1, 8, 3]
k = 3
```

Find the maximum sum of any contiguous subarray of size `k`.

### Hint

Do not recalculate each group from scratch.

Think:

``` text
remove left
add right
```

### Expected Answer

Windows:

``` text
[4,2,7] = 13
[2,7,1] = 10
[7,1,8] = 16
[1,8,3] = 12
```

Answer:

``` text
16
```

------------------------------------------------------------------------

# 62. FULL PRACTICE --- PAIR SUM IN SORTED ARRAY

## Problem

Determine whether a sorted array contains a pair whose sum equals
target.

### Input

``` text
arr = [1, 3, 4, 6, 8, 10]
target = 14
```

------------------------------------------------------------------------

## Thought Process

Because:

``` text
sorted + pair sum
```

we immediately consider:

``` text
two pointers
```

Start:

``` text
left = 0
right = 5
```

------------------------------------------------------------------------

## Dry Run

``` text
1 + 10 = 11
```

Too small:

``` text
left++
```

Now:

``` text
3 + 10 = 13
```

Too small:

``` text
left++
```

Now:

``` text
4 + 10 = 14
```

Found.

------------------------------------------------------------------------

## Code

``` java
public static boolean pairSum(int[] arr, int target) {

    int left = 0;
    int right = arr.length - 1;

    while (left < right) {

        int sum = arr[left] + arr[right];

        if (sum == target) {
            return true;
        }

        if (sum < target) {
            left++;
        } else {
            right--;
        }
    }

    return false;
}
```

------------------------------------------------------------------------

## Complexity

``` text
Time: O(n)
Space: O(1)
```

------------------------------------------------------------------------

# 63. FULL PRACTICE --- FIXED WINDOW

## Problem

Find the maximum average of any contiguous subarray of length `k`.

### Input

``` text
nums = [1, 12, -5, -6, 50, 3]
k = 4
```

Windows:

``` text
[1,12,-5,-6] = 2
[12,-5,-6,50] = 51
[-5,-6,50,3] = 42
```

Maximum average:

``` text
51 / 4 = 12.75
```

------------------------------------------------------------------------

## Code

``` java
public static double findMaxAverage(int[] nums, int k) {

    long sum = 0;

    for (int i = 0; i < k; i++) {
        sum += nums[i];
    }

    long maxSum = sum;

    for (int right = k; right < nums.length; right++) {

        sum += nums[right];
        sum -= nums[right - k];

        maxSum = Math.max(maxSum, sum);
    }

    return (double) maxSum / k;
}
```

------------------------------------------------------------------------

## Complexity

``` text
Time: O(n)
Space: O(1)
```

------------------------------------------------------------------------

# 64. FULL PRACTICE --- VARIABLE WINDOW

## Problem

Find the length of the longest substring without repeating characters.

### Input

``` text
s = "pwwkew"
```

Answer:

``` text
3
```

One valid longest substring:

``` text
"wke"
```

------------------------------------------------------------------------

## Approach

Maintain:

``` text
[left ... right]
```

with no duplicates.

If duplicate occurs:

``` text
remove from left
```

until valid.

------------------------------------------------------------------------

## Code

``` java
public static int longestUniqueSubstring(String s) {

    HashSet<Character> set = new HashSet<>();

    int left = 0;
    int answer = 0;

    for (int right = 0; right < s.length(); right++) {

        char ch = s.charAt(right);

        while (set.contains(ch)) {
            set.remove(s.charAt(left));
            left++;
        }

        set.add(ch);

        answer = Math.max(answer, right - left + 1);
    }

    return answer;
}
```

------------------------------------------------------------------------

# 65. PATTERN COMPARISON

  ------------------------------------------------------------------------
  Problem                                Brute Force Optimized Pattern
  --------------------- ---------------------------- ---------------------
  Pair sum sorted                              O(n²) Two pointers O(n)

  Remove duplicates      O(n) with extra structure / Slow-fast O(n), O(1)
                                   repeated handling 

  Move zeroes                         O(n²) possible Two pointers O(n)

  Max sum of k                                 O(nk) Fixed window O(n)

  Minimum valid                                O(n²) Variable window O(n)
  positive-sum window                                

  Longest unique                      O(n²) or worse Sliding window O(n)
  substring                                          

  Container With Most                          O(n²) Two pointers O(n)
  Water                                              

  3Sum                             O(n³) brute force Sort + two pointers
                                                     O(n²)
  ------------------------------------------------------------------------

------------------------------------------------------------------------

# 66. WHEN NOT TO USE SLIDING WINDOW

Do not see the word "subarray" and automatically use sliding window.

Ask:

### Question 1

Is the region contiguous?

If no:

``` text
Sliding window is probably not the right pattern.
```

### Question 2

Can the window property be maintained when moving `left` and `right`?

If no:

``` text
Look for another technique.
```

### Question 3

Does the condition behave predictably when expanding/shrinking?

For simple sum-based windows, positive numbers are especially important.

------------------------------------------------------------------------

# 67. 30-SECOND REVISION

## Two Pointers

``` text
Two indexes
↓
Avoid unnecessary pair checks
```

### Sorted pair sum

``` text
sum < target → left++
sum > target → right--
```

### Slow/Fast

``` text
fast scans
slow writes/marks useful position
```

------------------------------------------------------------------------

## Sliding Window

``` text
[left ... right]
```

### Fixed

``` text
window size = k
```

### Variable

``` text
expand right
shrink left when invalid
```

------------------------------------------------------------------------

# 68. MUST-MEMORIZE TEMPLATES

## Template 1 --- Sorted Pair

``` java
int left = 0;
int right = n - 1;

while (left < right) {

    int sum = arr[left] + arr[right];

    if (sum == target) {
        // found
        break;
    } else if (sum < target) {
        left++;
    } else {
        right--;
    }
}
```

------------------------------------------------------------------------

## Template 2 --- Fixed Window

``` java
int left = 0;
long sum = 0;

for (int right = 0; right < n; right++) {

    sum += arr[right];

    if (right - left + 1 > k) {
        sum -= arr[left];
        left++;
    }

    if (right - left + 1 == k) {
        // process
    }
}
```

------------------------------------------------------------------------

## Template 3 --- Variable Window

``` java
int left = 0;

for (int right = 0; right < n; right++) {

    // add right

    while (/* invalid */) {

        // remove left
        left++;
    }

    // process valid window
}
```

------------------------------------------------------------------------

## Template 4 --- Slow/Fast

``` java
int slow = 0;

for (int fast = 0; fast < n; fast++) {

    if (/* useful element */) {
        arr[slow] = arr[fast];
        slow++;
    }
}
```

------------------------------------------------------------------------

# 69. DAILY TEST --- 10 QUESTIONS

## Q1

A sorted array and a target pair sum usually suggests:

A. DFS\
B. Two pointers\
C. Dynamic programming\
D. Stack

------------------------------------------------------------------------

## Q2

For sorted pair sum, if:

``` text
sum < target
```

which pointer moves?

A. left\
B. right\
C. both\
D. neither

------------------------------------------------------------------------

## Q3

A fixed-size window of `k` elements is best handled using:

A. Fixed sliding window\
B. DFS\
C. Binary tree\
D. Recursion

------------------------------------------------------------------------

## Q4

When a variable window becomes invalid, we generally:

A. Reset the whole array\
B. Move right backward\
C. Move left forward\
D. Sort the window

------------------------------------------------------------------------

## Q5

What is the usual complexity of a single-pass two-pointer pair search on
a sorted array?

A. O(n³)\
B. O(n²)\
C. O(n log n)\
D. O(n)

------------------------------------------------------------------------

## Q6

Why can a sliding window be O(n) even when it contains a `while` loop?

A. The while loop never runs\
B. Both pointers move only forward, each at most O(n) times\
C. Java optimizes loops\
D. The array is always sorted

------------------------------------------------------------------------

## Q7

For:

``` text
maximum sum of exactly k consecutive elements
```

use:

A. Fixed window\
B. Binary search\
C. Recursion\
D. Stack

------------------------------------------------------------------------

## Q8

For:

``` text
longest substring satisfying a validity condition
```

a common pattern is:

A. Variable sliding window\
B. Selection sort\
C. Heap\
D. Binary tree

------------------------------------------------------------------------

## Q9

Can the simple positive-number minimum-subarray sliding-window logic
always be used when negative numbers are present?

A. Yes\
B. No

------------------------------------------------------------------------

## Q10

In a slow/fast pointer technique, the fast pointer usually:

A. Scans the input\
B. Always stays at zero\
C. Moves backward\
D. Sorts the array

------------------------------------------------------------------------

# 70. ANSWER KEY

``` text
Q1 → B
Q2 → A
Q3 → A
Q4 → C
Q5 → D
Q6 → B
Q7 → A
Q8 → A
Q9 → B
Q10 → A
```

------------------------------------------------------------------------

# 71. PATTERN RECOGNITION TEST

For each problem, identify the pattern **before coding**.

## Problem A

``` text
Sorted array
Find whether two values sum to target
```

Pattern:

``` text
____________________
```

------------------------------------------------------------------------

## Problem B

``` text
Maximum sum of exactly 5 consecutive elements
```

Pattern:

``` text
____________________
```

------------------------------------------------------------------------

## Problem C

``` text
Longest substring with at most k distinct characters
```

Pattern:

``` text
____________________
```

------------------------------------------------------------------------

## Problem D

``` text
Remove duplicates from sorted array in-place
```

Pattern:

``` text
____________________
```

------------------------------------------------------------------------

## Problem E

``` text
Minimum length subarray with sum >= target
All values are positive
```

Pattern:

``` text
____________________
```

------------------------------------------------------------------------

## Answers

``` text
A → Opposite-direction two pointers

B → Fixed sliding window

C → Variable sliding window

D → Slow/fast two pointers

E → Variable sliding window
```

------------------------------------------------------------------------

# 72. PLACEMENT PROBLEM CHECKLIST

Before submitting a solution, ask:

``` text
☐ Is the array sorted?
☐ Is this a pair problem?
☐ Can I use left/right pointers?
☐ Is this an in-place transformation?
☐ Can slow/fast pointers help?
☐ Is the problem about a contiguous region?
☐ Is the window size fixed?
☐ Is the window size variable?
☐ What makes the window valid?
☐ What makes the window invalid?
☐ When should I shrink?
☐ When should I update the answer?
☐ Can every pointer move only forward?
☐ What is the time complexity?
☐ What are the edge cases?
```

------------------------------------------------------------------------

# 73. PRACTICE PROBLEMS

The following problems are chosen to reinforce today's patterns.

## Easy

### 1. Two Sum II --- Input Array Is Sorted

Platform:

LeetCode

Difficulty:

Easy

Pattern:

Two pointers

What to notice:

The array is sorted, so you can use opposite-direction pointers.

Expected complexity:

``` text
O(n) time
O(1) extra space
```

Practice:

https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/

------------------------------------------------------------------------

### 2. Remove Duplicates from Sorted Array

Platform:

LeetCode

Difficulty:

Easy

Pattern:

Slow/Fast pointers

What to notice:

The array is sorted and the task is in-place.

Expected complexity:

``` text
O(n) time
O(1) extra space
```

Practice:

https://leetcode.com/problems/remove-duplicates-from-sorted-array/

------------------------------------------------------------------------

### 3. Move Zeroes

Platform:

LeetCode

Difficulty:

Easy

Pattern:

Slow/Fast pointers

What to notice:

Scan useful elements and place them at the next valid position.

Expected complexity:

``` text
O(n) time
O(1) extra space
```

Practice:

https://leetcode.com/problems/move-zeroes/

------------------------------------------------------------------------

### 4. Valid Palindrome

Platform:

LeetCode

Difficulty:

Easy

Pattern:

Opposite-direction two pointers

What to notice:

Compare from both ends while skipping invalid characters.

Expected complexity:

``` text
O(n) time
O(1) extra space
```

Practice:

https://leetcode.com/problems/valid-palindrome/

------------------------------------------------------------------------

## Medium

### 5. Container With Most Water

Platform:

LeetCode

Difficulty:

Medium

Pattern:

Two pointers

What to notice:

Move the pointer at the shorter height.

Expected complexity:

``` text
O(n) time
O(1) extra space
```

Practice:

https://leetcode.com/problems/container-with-most-water/

------------------------------------------------------------------------

### 6. 3Sum

Platform:

LeetCode

Difficulty:

Medium

Pattern:

Sorting + two pointers

What to notice:

Fix one value, then solve two-sum on the remaining range.

Expected complexity:

``` text
O(n²)
```

Practice:

https://leetcode.com/problems/3sum/

------------------------------------------------------------------------

### 7. Maximum Average Subarray I

Platform:

LeetCode

Difficulty:

Easy

Pattern:

Fixed sliding window

What to notice:

Only one element leaves and one enters as the window moves.

Expected complexity:

``` text
O(n) time
O(1) extra space
```

Practice:

https://leetcode.com/problems/maximum-average-subarray-i/

------------------------------------------------------------------------

### 8. Minimum Size Subarray Sum

Platform:

LeetCode

Difficulty:

Medium

Pattern:

Variable sliding window

What to notice:

The positive values make the sum predictable when expanding/shrinking.

Expected complexity:

``` text
O(n) time
O(1) extra space
```

Practice:

https://leetcode.com/problems/minimum-size-subarray-sum/

------------------------------------------------------------------------

### 9. Longest Substring Without Repeating Characters

Platform:

LeetCode

Difficulty:

Medium

Pattern:

Variable sliding window + HashSet

What to notice:

This is the Day 5 problem viewed through today's window pattern.

Expected complexity:

``` text
O(n) time
O(k) space
```

Practice:

https://leetcode.com/problems/longest-substring-without-repeating-characters/

------------------------------------------------------------------------

## Hard / Challenge

### 10. Trapping Rain Water

Platform:

LeetCode

Difficulty:

Hard

Pattern:

Two pointers

What to notice:

This is a more advanced pointer invariant problem.

Expected complexity for the two-pointer solution:

``` text
O(n) time
O(1) extra space
```

Practice:

https://leetcode.com/problems/trapping-rain-water/

------------------------------------------------------------------------

# 74. PRACTICE ORDER

Do not solve randomly.

Recommended order:

``` text
1. Two Sum II
       ↓
2. Remove Duplicates
       ↓
3. Move Zeroes
       ↓
4. Valid Palindrome
       ↓
5. Maximum Average Subarray I
       ↓
6. Minimum Size Subarray Sum
       ↓
7. Container With Most Water
       ↓
8. Longest Substring Without Repeating Characters
       ↓
9. 3Sum
       ↓
10. Trapping Rain Water
```

------------------------------------------------------------------------

# 75. HOMEWORK

Complete these without looking at the solution first:

### Homework 1

Write a two-pointer solution for:

``` text
Find whether a sorted array contains a pair with difference k.
```

Think about:

``` text
left
right
```

------------------------------------------------------------------------

### Homework 2

Write a fixed-window solution for:

``` text
Find the minimum sum of every contiguous window of size k.
```

------------------------------------------------------------------------

### Homework 3

Write a variable-window solution for:

``` text
Find the longest subarray containing at most 2 distinct values.
```

Hint:

``` text
HashMap + sliding window
```

------------------------------------------------------------------------

### Homework 4

Solve:

``` text
Container With Most Water
```

without looking at the editorial.

Before coding, explain:

> Why can we move the shorter side?

------------------------------------------------------------------------

# 76. QUICK REVISION SHEET

## Two Pointers

``` text
Two indexes
↓
Avoid repeated pair checks
```

### Opposite

``` text
left → ← right
```

Used for:

-   sorted pair sum
-   palindrome
-   container

### Same Direction

``` text
slow →
fast →
```

Used for:

-   remove duplicates
-   move zeroes
-   in-place filtering

------------------------------------------------------------------------

## Sliding Window

### Fixed

``` text
exactly k elements
```

Template:

``` text
add right
remove left
process
```

### Variable

``` text
longest/shortest valid region
```

Template:

``` text
expand right
while invalid:
    shrink left
update answer
```

------------------------------------------------------------------------

# 77. THE GOLDEN RULES

Memorize these.

> **Sorted + pair → Two Pointers**

> **In-place filtering → Slow/Fast Pointers**

> **Exactly k contiguous elements → Fixed Window**

> **Longest valid contiguous region → Variable Window**

> **Shortest valid contiguous region → Variable Window**

> **Expand until invalid → Shrink from left**

> **Every pointer moves forward at most n times → Often O(n)**

------------------------------------------------------------------------

# 78. DAY COMPLETION CHECKLIST

Do not mark Day 6 complete until you can explain these without notes.

``` text
☐ I understand what two pointers are
☐ I understand opposite-direction pointers
☐ I understand same-direction pointers
☐ I can solve pair sum in a sorted array
☐ I understand why sorting helps
☐ I can remove duplicates in-place
☐ I can move zeroes in-place
☐ I understand palindrome checking with two pointers
☐ I understand sliding window
☐ I know fixed vs variable windows
☐ I can solve maximum sum of k consecutive elements
☐ I understand why the fixed window is O(n)
☐ I understand variable-window expansion/shrinking
☐ I can solve minimum size subarray sum for positive numbers
☐ I understand longest unique substring as a sliding window
☐ I understand Container With Most Water
☐ I understand the basic 3Sum pattern
☐ I can recognize two-pointer clues
☐ I can recognize sliding-window clues
☐ I know when simple sliding window does not apply
☐ I completed the daily test
☐ I completed the pattern recognition test
☐ I completed the homework
☐ I solved the Easy practice problems
☐ I attempted at least 2 Medium problems
```

------------------------------------------------------------------------

# 79. DAY 6 MASTER SUMMARY

The most important lesson today is not a specific problem.

It is this:

> **Stop restarting your search when the next answer overlaps heavily
> with the previous one.**

Two pointers let you move intelligently through a sequence.

Sliding window lets you reuse information from an existing contiguous
region.

The progression you should recognize is:

``` text
Brute Force
   ↓
Repeated work
   ↓
Notice ordering / overlap
   ↓
Choose pointer movement
   ↓
Reuse previous information
   ↓
O(n) or O(n²) optimized solution
```

For placements, train yourself to immediately ask:

``` text
Is it sorted?
        ↓
Two pointers?

Is it contiguous?
        ↓
Sliding window?

Is the window exactly k?
        ↓
Fixed window?

Is the window longest/shortest valid?
        ↓
Variable window?

Do I need in-place filtering?
        ↓
Slow/Fast pointers?
```

If you can answer those questions quickly, you have learned the real
purpose of Day 6.

------------------------------------------------------------------------

# 80. NAVIGATION

**Previous:** [Day 5 --- Strings + Hashing](Day-05-Strings-Hashing.md)

**Next:** [Day 7 --- Sorting + Binary
Search](Day-07-Sorting-Binary-Search.md)

**Course:** Java DSA Placement Preparation

------------------------------------------------------------------------

# 🎯 DAY 6 COMPLETE

You have now learned:

``` text
Two Pointers
    ↓
Opposite direction
Same direction
Slow/Fast
Pair problems
In-place filtering

Sliding Window
    ↓
Fixed window
Variable window
Expand
Shrink
Maintain window state

Optimization
    ↓
Brute Force
    ↓
Identify repeated work
    ↓
Reuse information
    ↓
Optimized solution
```

**Do not move to Day 7 until you can identify the pattern before writing
code.**
