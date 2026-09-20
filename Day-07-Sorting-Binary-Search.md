# 🔥 DAY 7 --- SORTING + BINARY SEARCH

## Today's Goal

Today you will learn two extremely important placement patterns:

> **Sorting**

> **Binary Search**

By the end of today, you should be able to:

-   Understand why sorting is useful
-   Compare common sorting algorithms
-   Implement Bubble Sort, Selection Sort, Insertion Sort, Merge Sort,
    and Quick Sort
-   Understand `Arrays.sort()`
-   Understand stable and in-place sorting at interview level
-   Perform standard binary search
-   Avoid binary-search off-by-one errors
-   Find first and last occurrence
-   Understand lower bound and upper bound
-   Find insertion position
-   Search rotated sorted arrays
-   Recognize binary search on answer
-   Identify monotonic feasibility
-   Convert brute-force search into `O(log n)` or `O(n log n)` solutions

------------------------------------------------------------------------

# 1. PREREQUISITES

You should already know:

-   Java loops
-   Methods
-   Arrays
-   Time and space complexity
-   Two pointers
-   Basic problem-solving patterns

You do **not** need to relearn arrays or loops today. We will use them
as building blocks.

------------------------------------------------------------------------

# 2. PRIORITY

  Topic                     Priority
  ------------------------- ------------
  Sorting fundamentals      🔥🔥🔥🔥
  `Arrays.sort()`           🔥🔥🔥🔥🔥
  Bubble Sort               🔥🔥
  Selection Sort            🔥🔥
  Insertion Sort            🔥🔥🔥
  Merge Sort                🔥🔥🔥🔥
  Quick Sort                🔥🔥🔥🔥
  Binary Search             🔥🔥🔥🔥🔥
  First/Last Occurrence     🔥🔥🔥🔥
  Lower/Upper Bound         🔥🔥🔥🔥
  Rotated Array Search      🔥🔥🔥🔥
  Binary Search on Answer   🔥🔥🔥🔥🔥
  Pattern Recognition       🔥🔥🔥🔥🔥

------------------------------------------------------------------------

# 3. WHY SORTING?

## 🧑‍🎓 Beginner Explanation

Sorting means arranging data in an order.

Example:

``` text
Before:
[5, 2, 8, 1, 3]

After:
[1, 2, 3, 5, 8]
```

Common orders:

``` text
Ascending:
1 2 3 4 5

Descending:
5 4 3 2 1
```

But in DSA, sorting is important for more than making values look
organized.

Sorting can unlock:

``` text
Binary Search
Two Pointers
Greedy Algorithms
Duplicate grouping
Interval processing
Easier comparisons
```

So think of sorting as:

> **A preprocessing step that creates useful structure.**

------------------------------------------------------------------------

# 4. SORTING AS PREPROCESSING

Suppose:

``` text
arr = [8, 2, 7, 1, 5]
```

After sorting:

``` text
[1, 2, 5, 7, 8]
```

Now many operations become easier.

For example:

``` text
Find 7
```

Instead of checking every value, binary search can eliminate half the
search space repeatedly.

Another example:

``` text
Find two numbers with target sum
```

After sorting, two pointers can be used.

So:

``` text
Sort
  ↓
Create order
  ↓
Use another efficient pattern
```

------------------------------------------------------------------------

# 5. IMPORTANT SORTING TERMS

## Stable Sorting

A stable sort preserves the relative order of equal-key records.

Example:

``` text
(A, 90)
(B, 90)
(C, 80)
```

Sorting by score using a stable sort gives:

``` text
(C, 80)
(A, 90)
(B, 90)
```

`A` remains before `B`.

### Interview definition

> A stable sorting algorithm preserves the relative order of elements
> having equal keys.

------------------------------------------------------------------------

## In-Place Sorting

An in-place algorithm uses little additional memory beyond the input.

Examples:

``` text
Selection Sort → O(1) extra space
Insertion Sort → O(1) extra space
```

------------------------------------------------------------------------

# 6. BUBBLE SORT

## 🧑‍🎓 Beginner Explanation

Bubble Sort repeatedly compares adjacent elements.

If they are in the wrong order:

``` text
swap
```

The larger values gradually move toward the end.

Example:

``` text
[5, 1, 4, 2]
```

Compare:

``` text
5 and 1
```

Swap:

``` text
[1, 5, 4, 2]
```

Then:

``` text
5 and 4
```

Swap:

``` text
[1, 4, 5, 2]
```

Then:

``` text
5 and 2
```

Swap:

``` text
[1, 4, 2, 5]
```

The largest value has reached the end.

------------------------------------------------------------------------

# 7. BUBBLE SORT VISUALIZATION

``` text
[5, 1, 4, 2]

Pass 1:
5 1 → swap
1 5 4 2

5 4 → swap
1 4 5 2

5 2 → swap
1 4 2 5

Largest value is now fixed.
```

Then repeat for the remaining portion.

------------------------------------------------------------------------

# 8. BUBBLE SORT JAVA

``` java
public static void bubbleSort(int[] arr) {

    int n = arr.length;

    for (int i = 0; i < n - 1; i++) {

        boolean swapped = false;

        for (int j = 0; j < n - 1 - i; j++) {

            if (arr[j] > arr[j + 1]) {

                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;

                swapped = true;
            }
        }

        // Already sorted
        if (!swapped) {
            break;
        }
    }
}
```

------------------------------------------------------------------------

# 9. BUBBLE SORT COMPLEXITY

  Case          Complexity
  ------------- ----------------------------
  Best          `O(n)` with early stopping
  Average       `O(n²)`
  Worst         `O(n²)`
  Extra Space   `O(1)`

### Important

Bubble Sort is mainly useful for:

-   Learning sorting
-   Understanding swapping
-   Basic interview questions

For normal Java coding, use an efficient library sort unless the problem
asks for a custom implementation.

------------------------------------------------------------------------

# 10. SELECTION SORT

## 🧑‍🎓 Beginner Explanation

Selection Sort repeatedly finds the smallest element from the unsorted
part and puts it into the correct position.

Example:

``` text
[5, 2, 4, 1, 3]
```

Find minimum:

``` text
1
```

Put it at index `0`:

``` text
[1, 2, 4, 5, 3]
```

Then process the remaining portion.

------------------------------------------------------------------------

# 11. SELECTION SORT VISUALIZATION

``` text
Sorted | Unsorted

[ ] | [5, 2, 4, 1, 3]
      minimum = 1

[1] | [2, 4, 5, 3]

[1,2] | [4,5,3]

[1,2,3] | [5,4]

[1,2,3,4,5]
```

------------------------------------------------------------------------

# 12. SELECTION SORT JAVA

``` java
public static void selectionSort(int[] arr) {

    int n = arr.length;

    for (int i = 0; i < n - 1; i++) {

        int minIndex = i;

        for (int j = i + 1; j < n; j++) {

            if (arr[j] < arr[minIndex]) {
                minIndex = j;
            }
        }

        int temp = arr[i];
        arr[i] = arr[minIndex];
        arr[minIndex] = temp;
    }
}
```

------------------------------------------------------------------------

# 13. SELECTION SORT COMPLEXITY

``` text
Best:    O(n²)
Average: O(n²)
Worst:   O(n²)
Space:   O(1)
```

Unlike optimized Bubble Sort, an already sorted array does not make
Selection Sort linear.

------------------------------------------------------------------------

# 14. INSERTION SORT

## 🧑‍🎓 Beginner Explanation

Insertion Sort builds a sorted section one element at a time.

Think about arranging playing cards.

Suppose you already have:

``` text
[2, 5, 7]
```

and receive:

``` text
4
```

You insert it between `2` and `5`:

``` text
[2, 4, 5, 7]
```

------------------------------------------------------------------------

# 15. INSERTION SORT VISUALIZATION

``` text
[2 | 5 7 3 8]

2 is sorted.

Take 5:
[2 5 | 7 3 8]

Take 7:
[2 5 7 | 3 8]

Take 3:
shift 7
shift 5

[2 3 5 7 | 8]
```

------------------------------------------------------------------------

# 16. INSERTION SORT JAVA

``` java
public static void insertionSort(int[] arr) {

    for (int i = 1; i < arr.length; i++) {

        int key = arr[i];
        int j = i - 1;

        while (j >= 0 && arr[j] > key) {

            arr[j + 1] = arr[j];
            j--;
        }

        arr[j + 1] = key;
    }
}
```

------------------------------------------------------------------------

# 17. INSERTION SORT COMPLEXITY

``` text
Best:    O(n)
Average: O(n²)
Worst:   O(n²)
Space:   O(1)
```

Insertion Sort can be useful when:

-   The input is small
-   The input is nearly sorted
-   You need a simple in-place sort

------------------------------------------------------------------------

# 18. SORTING ALGORITHM COMPARISON

  Algorithm             Best      Average        Worst   Extra Space
  ----------- -------------- ------------ ------------ -------------
  Bubble                O(n)        O(n²)        O(n²)          O(1)
  Selection            O(n²)        O(n²)        O(n²)          O(1)
  Insertion             O(n)        O(n²)        O(n²)          O(1)
  Merge           O(n log n)   O(n log n)   O(n log n)          O(n)
  Quick         O(n log n)\*   O(n log n)      O(n²)\*    O(log n)\*

`*` depends on implementation and pivot behavior.

------------------------------------------------------------------------

# 19. MERGE SORT

Now we move to an efficient sorting algorithm.

Merge Sort uses:

> **Divide and Conquer**

The idea:

``` text
Array
  ↓
Divide
  ↓
Sort left half
Sort right half
  ↓
Merge
```

------------------------------------------------------------------------

# 20. MERGE SORT VISUALIZATION

Input:

``` text
[8, 3, 2, 9, 7, 1, 5, 4]
```

Split:

``` text
[8,3,2,9] [7,1,5,4]
```

Again:

``` text
[8,3] [2,9] [7,1] [5,4]
```

Again:

``` text
[8] [3] [2] [9] [7] [1] [5] [4]
```

A single element is already sorted.

Now merge:

``` text
[3,8]
[2,9]
[1,7]
[4,5]
```

Then:

``` text
[2,3,8,9]
[1,4,5,7]
```

Finally:

``` text
[1,2,3,4,5,7,8,9]
```

------------------------------------------------------------------------

# 21. MERGING TWO SORTED ARRAYS

Suppose:

``` text
left  = [2,5,8]
right = [1,4,9]
```

Compare the first elements:

``` text
2 vs 1 → take 1
```

Then:

``` text
2 vs 4 → take 2
```

Then:

``` text
5 vs 4 → take 4
```

Then:

``` text
5 vs 9 → take 5
```

Then:

``` text
8 vs 9 → take 8
```

Finally:

``` text
9
```

Result:

``` text
[1,2,4,5,8,9]
```

Merging takes:

``` text
O(n)
```

for the number of elements being merged.

------------------------------------------------------------------------

# 22. MERGE SORT JAVA

``` java
public static void mergeSort(int[] arr) {

    if (arr.length <= 1) {
        return;
    }

    int[] temp = new int[arr.length];

    mergeSort(arr, temp, 0, arr.length - 1);
}

private static void mergeSort(
        int[] arr,
        int[] temp,
        int left,
        int right) {

    if (left >= right) {
        return;
    }

    int mid = left + (right - left) / 2;

    mergeSort(arr, temp, left, mid);
    mergeSort(arr, temp, mid + 1, right);

    merge(arr, temp, left, mid, right);
}

private static void merge(
        int[] arr,
        int[] temp,
        int left,
        int mid,
        int right) {

    int i = left;
    int j = mid + 1;
    int k = left;

    while (i <= mid && j <= right) {

        if (arr[i] <= arr[j]) {
            temp[k++] = arr[i++];
        } else {
            temp[k++] = arr[j++];
        }
    }

    while (i <= mid) {
        temp[k++] = arr[i++];
    }

    while (j <= right) {
        temp[k++] = arr[j++];
    }

    for (int index = left; index <= right; index++) {
        arr[index] = temp[index];
    }
}
```

------------------------------------------------------------------------

# 23. WHY USE `<=` DURING MERGE?

This:

``` java
if (arr[i] <= arr[j])
```

takes the left element first when values are equal.

That helps preserve stability.

This is one reason Merge Sort can be implemented as a stable sort.

------------------------------------------------------------------------

# 24. MERGE SORT COMPLEXITY

At every recursion level, the total merging work is approximately:

``` text
O(n)
```

The number of levels is:

``` text
O(log n)
```

Therefore:

``` text
O(n log n)
```

Complexity:

``` text
Best:    O(n log n)
Average: O(n log n)
Worst:   O(n log n)
Space:   O(n)
```

------------------------------------------------------------------------

# 25. WHY `mid = left + (right - left) / 2`?

Instead of:

``` java
int mid = (left + right) / 2;
```

prefer:

``` java
int mid = left + (right - left) / 2;
```

It avoids potential integer overflow in extreme index ranges.

You should memorize this form because it is also used in binary search.

------------------------------------------------------------------------

# 26. QUICK SORT

Quick Sort also uses divide and conquer.

Main idea:

``` text
Choose pivot
      ↓
Partition
      ↓
Smaller values | pivot | Larger values
      ↓
Recursively sort both sides
```

------------------------------------------------------------------------

# 27. QUICK SORT EXAMPLE

Input:

``` text
[5,2,8,1,4]
```

Suppose:

``` text
pivot = 4
```

After partitioning, one possible arrangement is:

``` text
[2,1] 4 [5,8]
```

Then recursively sort:

``` text
[2,1]
[5,8]
```

------------------------------------------------------------------------

# 28. QUICK SORT JAVA

``` java
public static void quickSort(int[] arr) {
    quickSort(arr, 0, arr.length - 1);
}

private static void quickSort(
        int[] arr,
        int low,
        int high) {

    if (low >= high) {
        return;
    }

    int pivotIndex = partition(arr, low, high);

    quickSort(arr, low, pivotIndex - 1);
    quickSort(arr, pivotIndex + 1, high);
}

private static int partition(
        int[] arr,
        int low,
        int high) {

    int pivot = arr[high];
    int i = low;

    for (int j = low; j < high; j++) {

        if (arr[j] <= pivot) {

            int temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;

            i++;
        }
    }

    int temp = arr[i];
    arr[i] = arr[high];
    arr[high] = temp;

    return i;
}
```

------------------------------------------------------------------------

# 29. QUICK SORT COMPLEXITY

``` text
Average: O(n log n)
Worst:   O(n²)
```

Worst case can occur when partitions are very unbalanced.

Example:

``` text
n-1 elements | pivot | 0 elements
```

repeatedly.

Good pivot selection strategies reduce the likelihood of bad partitions.

------------------------------------------------------------------------

# 30. MERGE SORT VS QUICK SORT

  Feature                   Merge Sort       Quick Sort
  ------------------------- ---------------- ----------------------------
  Average                   O(n log n)       O(n log n)
  Worst                     O(n log n)       O(n²)
  Extra array               Usually yes      Usually no
  Main idea                 Divide + merge   Pivot + partition
  Stable                    Can be stable    Usually not
  Typical auxiliary space   O(n)             O(log n) average recursion

For placement interviews, know the **idea + complexity + trade-off**.

------------------------------------------------------------------------

# 31. BUILT-IN JAVA SORTING

For most coding questions:

``` java
Arrays.sort(arr);
```

is the practical choice when custom sorting is not requested.

Example:

``` java
int[] arr = {5, 2, 8, 1, 3};

Arrays.sort(arr);

System.out.println(Arrays.toString(arr));
```

Output:

``` text
[1, 2, 3, 5, 8]
```

------------------------------------------------------------------------

# 32. SORTING A LIST

``` java
List<Integer> list = new ArrayList<>();

list.add(5);
list.add(1);
list.add(3);

Collections.sort(list);
```

Or:

``` java
list.sort(Integer::compareTo);
```

Descending:

``` java
list.sort(Collections.reverseOrder());
```

------------------------------------------------------------------------

# 33. WHEN SHOULD YOU WRITE YOUR OWN SORT?

Use a custom sorting implementation when:

-   The interviewer explicitly asks for it
-   The assessment is testing sorting implementation
-   You need a special algorithmic property
-   The problem requires controlling the sorting process

Otherwise:

``` java
Arrays.sort(arr);
```

is normally simpler and less error-prone.

------------------------------------------------------------------------

# 34. BINARY SEARCH

## 🧑‍🎓 Beginner Explanation

Binary Search searches an ordered search space by repeatedly eliminating
about half of the remaining possibilities.

Example:

``` text
[1,3,5,7,9,11,13]
```

Target:

``` text
11
```

Start in the middle:

``` text
7
```

Since:

``` text
11 > 7
```

discard everything on the left.

Now search:

``` text
[9,11,13]
```

Middle:

``` text
11
```

Found.

------------------------------------------------------------------------

# 35. LINEAR SEARCH VS BINARY SEARCH

Linear Search:

``` text
Check one by one
```

Complexity:

``` text
O(n)
```

Binary Search:

``` text
Discard half each time
```

Complexity:

``` text
O(log n)
```

For:

``` text
n = 1,000,000
```

linear search may need up to about:

``` text
1,000,000
```

checks.

Binary search needs only around:

``` text
20
```

halving steps.

------------------------------------------------------------------------

# 36. WHY O(log n)?

Search space:

``` text
n
n/2
n/4
n/8
...
1
```

Each step divides the possibilities by approximately 2.

Therefore:

``` text
Time = O(log₂ n)
```

------------------------------------------------------------------------

# 37. STANDARD BINARY SEARCH

## Algorithm

``` text
left = 0
right = n - 1

while left <= right:

    mid

    if arr[mid] == target:
        found

    if arr[mid] < target:
        search right half

    else:
        search left half
```

------------------------------------------------------------------------

# 38. JAVA --- STANDARD BINARY SEARCH

``` java
public static int binarySearch(int[] arr, int target) {

    int left = 0;
    int right = arr.length - 1;

    while (left <= right) {

        int mid = left + (right - left) / 2;

        if (arr[mid] == target) {
            return mid;
        }

        if (arr[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }

    return -1;
}
```

------------------------------------------------------------------------

# 39. DRY RUN

Input:

``` text
arr = [1,3,5,7,9,11,13]
target = 11
```

Initial:

``` text
left = 0
right = 6
mid = 3
```

``` text
arr[mid] = 7
```

Since:

``` text
7 < 11
```

move:

``` text
left = 4
```

Now:

``` text
left = 4
right = 6
mid = 5
```

``` text
arr[5] = 11
```

Found.

Answer:

``` text
5
```

------------------------------------------------------------------------

# 40. COMPLEXITY

``` text
Time:  O(log n)
Space: O(1)
```

------------------------------------------------------------------------

# 41. BINARY SEARCH INVARIANT

This is the best way to understand binary search.

For the standard inclusive version:

``` text
[left, right]
```

represents the remaining possible search space.

The invariant is:

> If the target exists, it is still inside the current search range.

Therefore:

``` java
left = mid + 1;
```

means:

> Everything up to and including `mid` has been eliminated.

And:

``` java
right = mid - 1;
```

means:

> Everything from `mid` onward has been eliminated.

This mental model is more useful than memorizing random pointer
movements.

------------------------------------------------------------------------

# 42. BINARY SEARCH INTERVAL STYLES

Two common styles are:

### Closed interval

``` text
[left, right]
```

Typical template:

``` java
while (left <= right)
```

and:

``` java
right = mid - 1;
left = mid + 1;
```

### Half-open interval

``` text
[left, right)
```

Typical boundary searches use:

``` java
while (left < right)
```

Do not mix these styles without understanding their meaning.

For beginners, master the closed interval first.

------------------------------------------------------------------------

# 43. FIRST OCCURRENCE

Example:

``` text
arr = [1,2,2,2,4,5]
target = 2
```

Normal binary search can return any occurrence.

But if the problem asks for the **first** occurrence:

When you find the target:

``` text
save mid
continue left
```

------------------------------------------------------------------------

# 44. FIRST OCCURRENCE JAVA

``` java
public static int firstOccurrence(int[] arr, int target) {

    int left = 0;
    int right = arr.length - 1;
    int answer = -1;

    while (left <= right) {

        int mid = left + (right - left) / 2;

        if (arr[mid] == target) {

            answer = mid;
            right = mid - 1;

        } else if (arr[mid] < target) {

            left = mid + 1;

        } else {

            right = mid - 1;
        }
    }

    return answer;
}
```

------------------------------------------------------------------------

# 45. LAST OCCURRENCE

For last occurrence:

When target is found:

``` text
save mid
continue right
```

``` java
public static int lastOccurrence(int[] arr, int target) {

    int left = 0;
    int right = arr.length - 1;
    int answer = -1;

    while (left <= right) {

        int mid = left + (right - left) / 2;

        if (arr[mid] == target) {

            answer = mid;
            left = mid + 1;

        } else if (arr[mid] < target) {

            left = mid + 1;

        } else {

            right = mid - 1;
        }
    }

    return answer;
}
```

------------------------------------------------------------------------

# 46. COUNT OCCURRENCES

Once you know:

``` text
first
last
```

the count is:

``` text
last - first + 1
```

Example:

``` text
arr = [1,2,2,2,4]
target = 2
```

``` text
first = 1
last = 3
```

Therefore:

``` text
3 - 1 + 1 = 3
```

------------------------------------------------------------------------

# 47. LOWER BOUND

Lower bound means:

> **First index whose value is greater than or equal to target.**

Example:

``` text
arr = [1,3,3,5,7]
target = 4
```

First value `>= 4`:

``` text
5
```

Index:

``` text
3
```

------------------------------------------------------------------------

# 48. LOWER BOUND JAVA

``` java
public static int lowerBound(int[] arr, int target) {

    int left = 0;
    int right = arr.length;

    while (left < right) {

        int mid = left + (right - left) / 2;

        if (arr[mid] >= target) {
            right = mid;
        } else {
            left = mid + 1;
        }
    }

    return left;
}
```

Notice:

``` text
right = n
```

because the answer can legally be `n`.

Example:

``` text
arr = [1,2,3]
target = 10
```

There is no value `>= 10`.

The insertion/boundary position is:

``` text
3
```

------------------------------------------------------------------------

# 49. UPPER BOUND

Upper bound means:

> **First index whose value is strictly greater than target.**

Example:

``` text
arr = [1,3,3,5,7]
target = 3
```

First value `> 3`:

``` text
5
```

Index:

``` text
3
```

------------------------------------------------------------------------

# 50. UPPER BOUND JAVA

``` java
public static int upperBound(int[] arr, int target) {

    int left = 0;
    int right = arr.length;

    while (left < right) {

        int mid = left + (right - left) / 2;

        if (arr[mid] > target) {
            right = mid;
        } else {
            left = mid + 1;
        }
    }

    return left;
}
```

------------------------------------------------------------------------

# 51. LOWER VS UPPER BOUND

Memorize:

``` text
Lower Bound
→ first >= target

Upper Bound
→ first > target
```

Example:

``` text
[1,2,2,2,5]
target = 2
```

``` text
lowerBound = 1
upperBound = 4
```

Count:

``` text
upperBound - lowerBound
= 4 - 1
= 3
```

------------------------------------------------------------------------

# 52. SEARCH INSERT POSITION

Problem:

> Find the position where target should be inserted into a sorted array.

Example:

``` text
nums = [1,3,5,6]
target = 2
```

Insert:

``` text
[1,2,3,5,6]
```

Answer:

``` text
1
```

This is essentially:

``` text
lower bound
```

------------------------------------------------------------------------

# 53. SEARCH INSERT JAVA

``` java
public static int searchInsert(int[] nums, int target) {

    int left = 0;
    int right = nums.length;

    while (left < right) {

        int mid = left + (right - left) / 2;

        if (nums[mid] >= target) {
            right = mid;
        } else {
            left = mid + 1;
        }
    }

    return left;
}
```

------------------------------------------------------------------------

# 54. ROTATED SORTED ARRAY

Classic example:

``` text
Original:
[0,1,2,4,5,6,7]

Rotated:
[4,5,6,7,0,1,2]
```

The whole array is not sorted.

But an important property remains:

> **At least one half around `mid` is sorted.**

This lets us discard half of the search space.

------------------------------------------------------------------------

# 55. ROTATED ARRAY VISUALIZATION

``` text
[4,5,6,7,0,1,2]
 L     M       R
```

If:

``` java
nums[left] <= nums[mid]
```

then the left half is sorted.

Now ask:

``` text
Is target between nums[left] and nums[mid]?
```

If yes:

``` java
right = mid - 1;
```

Otherwise:

``` java
left = mid + 1;
```

If the right half is sorted, use the symmetric logic.

------------------------------------------------------------------------

# 56. SEARCH ROTATED ARRAY JAVA

``` java
public static int searchRotated(int[] nums, int target) {

    int left = 0;
    int right = nums.length - 1;

    while (left <= right) {

        int mid = left + (right - left) / 2;

        if (nums[mid] == target) {
            return mid;
        }

        // Left half is sorted.
        if (nums[left] <= nums[mid]) {

            if (nums[left] <= target && target < nums[mid]) {
                right = mid - 1;
            } else {
                left = mid + 1;
            }

        } else {

            // Right half is sorted.
            if (nums[mid] < target && target <= nums[right]) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
    }

    return -1;
}
```

------------------------------------------------------------------------

# 57. COMPLEXITY

For the standard distinct-value rotated-array problem:

``` text
Time:  O(log n)
Space: O(1)
```

Duplicates can make the problem more complicated because it may become
impossible to determine which half is strictly sorted in some cases.

------------------------------------------------------------------------

# 58. BINARY SEARCH ON ANSWER

This is one of the most important placement patterns.

Sometimes the array itself is not sorted.

Instead, the **answer space** has a monotonic property.

Example:

``` text
Candidate answer:

1 → false
2 → false
3 → false
4 → true
5 → true
6 → true
```

This looks like:

``` text
F F F T T T
```

There is a boundary.

Binary search can find the first `T`.

------------------------------------------------------------------------

# 59. WHAT DOES MONOTONIC MEAN?

A condition is monotonic when, after it changes in one direction, it
never changes back.

For example:

``` text
false false false true true true
```

Once it becomes true, every larger value remains true.

Or:

``` text
true true true false false false
```

Once it becomes false, every larger value remains false.

This is the structure binary search needs.

------------------------------------------------------------------------

# 60. BINARY SEARCH ON ANSWER TEMPLATE

``` java
long left = minimumAnswer;
long right = maximumAnswer;

while (left < right) {

    long mid = left + (right - left) / 2;

    if (isPossible(mid)) {
        right = mid;
    } else {
        left = mid + 1;
    }
}

return left;
```

The difficult part is usually:

``` java
isPossible(mid)
```

You must correctly define what makes a candidate answer feasible.

------------------------------------------------------------------------

# 61. EXAMPLE --- KOKO EATING BANANAS

Suppose:

``` text
piles = [3,6,7,11]
h = 8
```

We want the minimum eating speed.

Search range:

``` text
1 ... 11
```

At a speed that is too low:

``` text
cannot finish
```

At a sufficiently high speed:

``` text
can finish
```

So the feasibility pattern is:

``` text
false false false true true true
```

Binary search finds the first true value.

------------------------------------------------------------------------

# 62. JAVA --- KOKO STYLE

``` java
public static int minEatingSpeed(int[] piles, int h) {

    int left = 1;
    int right = 0;

    for (int pile : piles) {
        right = Math.max(right, pile);
    }

    while (left < right) {

        int mid = left + (right - left) / 2;

        if (canFinish(piles, h, mid)) {
            right = mid;
        } else {
            left = mid + 1;
        }
    }

    return left;
}

private static boolean canFinish(
        int[] piles,
        int h,
        int speed) {

    long hours = 0;

    for (int pile : piles) {

        hours += (pile + (long) speed - 1) / speed;

        if (hours > h) {
            return false;
        }
    }

    return true;
}
```

------------------------------------------------------------------------

# 63. WHY CEILING DIVISION?

We need:

``` text
ceil(pile / speed)
```

For positive integers:

``` java
(pile + speed - 1) / speed
```

Example:

``` text
pile = 7
speed = 3
```

Normal integer division:

``` text
7 / 3 = 2
```

But required:

``` text
ceil(7 / 3) = 3
```

So:

``` text
(7 + 3 - 1) / 3
= 9 / 3
= 3
```

------------------------------------------------------------------------

# 64. BRUTE FORCE → OPTIMAL

## Example 1 --- Search

Brute force:

``` text
Check every element
```

Complexity:

``` text
O(n)
```

Sorted array:

``` text
Binary Search
```

Complexity:

``` text
O(log n)
```

------------------------------------------------------------------------

## Example 2 --- Pair Sum

Brute force:

``` text
Try every pair
O(n²)
```

Sorted:

``` text
Two pointers
O(n)
```

If sorting is required:

``` text
O(n log n) + O(n)
= O(n log n)
```

------------------------------------------------------------------------

## Example 3 --- Search for Minimum Feasible Answer

Brute force:

``` text
Try every possible answer
```

If the answer range is huge, this can be too slow.

Instead:

``` text
Find monotonic feasibility
        ↓
Binary Search
        ↓
O(log answerRange) feasibility checks
```

------------------------------------------------------------------------

# 65. SORTING + BINARY SEARCH

Sometimes the workflow is:

``` text
Input
 ↓
Sort
 ↓
Binary Search repeatedly
```

If sorting costs:

``` text
O(n log n)
```

and each search costs:

``` text
O(log n)
```

then after sorting, many searches can be performed efficiently.

This is especially useful when:

-   The data is reused
-   There are many queries
-   Sorting is allowed
-   Original order is not required

------------------------------------------------------------------------

# 66. SORTING + TWO POINTERS

Connect today's lesson with Day 6.

Suppose:

``` text
arr = [8,1,6,3,5]
```

For pair-related problems:

``` text
Sort
 ↓
[1,3,5,6,8]
 ↓
Two pointers
```

Complexity:

``` text
Sorting = O(n log n)
Two pointers = O(n)
Overall = O(n log n)
```

This combination is extremely common.

------------------------------------------------------------------------

# 67. COMMON SORTING MISTAKES

## Mistake 1 --- Using O(n²) sorting unnecessarily

If:

``` text
n = 100000
```

Bubble Sort may be far too slow.

Use:

``` java
Arrays.sort(arr);
```

when allowed.

------------------------------------------------------------------------

## Mistake 2 --- Forgetting that sorting changes the array

``` java
Arrays.sort(arr);
```

mutates the array.

If original order matters, copy first:

``` java
int[] copy = arr.clone();
Arrays.sort(copy);
```

------------------------------------------------------------------------

## Mistake 3 --- Sorting when original indices are needed

Suppose:

``` text
Find two values and return their original indices.
```

Sorting can destroy index information unless you preserve it.

------------------------------------------------------------------------

## Mistake 4 --- Assuming all sorting algorithms are O(n log n)

Not true.

``` text
Bubble → O(n²)
Selection → O(n²)
Insertion → O(n²) worst
Merge → O(n log n)
Quick → O(n log n) average
```

------------------------------------------------------------------------

# 68. COMMON BINARY SEARCH MISTAKES

## Mistake 1 --- Wrong loop condition

For the standard closed interval:

``` java
while (left <= right)
```

------------------------------------------------------------------------

## Mistake 2 --- Wrong pointer movement

Use:

``` java
left = mid + 1;
right = mid - 1;
```

when eliminating `mid`.

------------------------------------------------------------------------

## Mistake 3 --- Integer overflow in midpoint

Prefer:

``` java
int mid = left + (right - left) / 2;
```

------------------------------------------------------------------------

## Mistake 4 --- Returning immediately for boundary problems

For first occurrence:

``` text
found
↓
save
↓
continue left
```

For last occurrence:

``` text
found
↓
save
↓
continue right
```

------------------------------------------------------------------------

## Mistake 5 --- Using binary search without order

Binary search needs:

``` text
sorted structure
```

or:

``` text
monotonic feasibility
```

Do not force it onto arbitrary unsorted data.

------------------------------------------------------------------------

# 69. EDGE CASES

Always test:

``` text
[]
[5]
[1,2]
target is minimum
target is maximum
target absent
duplicate target
all values equal
already sorted
reverse sorted
rotated sorted
rotation near beginning
rotation near end
```

For boundary search, test:

``` text
target before all elements
target after all elements
target between values
target equal to first
target equal to last
```

------------------------------------------------------------------------

# 70. JAVA-SPECIFIC NOTES

## Primitive array sort

``` java
Arrays.sort(arr);
```

## Print array

``` java
System.out.println(Arrays.toString(arr));
```

## Sort a list

``` java
Collections.sort(list);
```

## Descending list

``` java
list.sort(Collections.reverseOrder());
```

For primitive `int[]`, `Collections.reverseOrder()` is not directly
applicable because primitive arrays are not collections.

------------------------------------------------------------------------

# 71. INTERVIEW EXPLANATION --- SORTING

If asked:

> Why did you sort the array?

Answer:

> "Sorting creates useful order that can simplify the remaining problem.
> It can enable binary search, two pointers, duplicate grouping, greedy
> decisions, or interval processing. I also consider the sorting cost,
> typically O(n log n) for an efficient comparison sort."

------------------------------------------------------------------------

# 72. INTERVIEW EXPLANATION --- BINARY SEARCH

Answer:

> "The search space has an ordering property. By comparing the target
> with the middle element, I can eliminate approximately half of the
> remaining candidates after every comparison. Therefore the search
> takes O(log n) time."

------------------------------------------------------------------------

# 73. INTERVIEW EXPLANATION --- BINARY SEARCH ON ANSWER

Answer:

> "The values themselves are not necessarily sorted, but the feasibility
> of a candidate answer is monotonic. Once a candidate becomes feasible,
> larger candidates remain feasible, or the reverse. Therefore I can
> binary-search the answer range using a feasibility function."

------------------------------------------------------------------------

# 74. CONSTRAINT THINKING

Look at `n` before choosing an algorithm.

### Small `n`

``` text
n <= 100
```

`O(n²)` may be acceptable.

### Medium `n`

``` text
n ≈ 10³
```

`O(n²)` may sometimes be acceptable.

### Large `n`

``` text
n ≈ 10⁵
```

Prefer:

``` text
O(n)
O(n log n)
```

### Huge answer range

If the answer can be very large:

``` text
1 ... 10^9
```

and feasibility is monotonic:

``` text
Binary Search on Answer
```

is worth checking.

------------------------------------------------------------------------

# 75. DECISION TREE --- SORTING

``` text
Need ordered values?
        |
       YES
        |
Can built-in sorting be used?
        |
       YES
        ↓
 Arrays.sort()
        |
       NO
        ↓
Is sorting implementation being tested?
        |
       YES
        ↓
Choose required algorithm
```

------------------------------------------------------------------------

# 76. DECISION TREE --- BINARY SEARCH

``` text
Is the search space ordered?
        |
       YES
        ↓
Binary Search

Is there a monotonic true/false condition?
        |
       YES
        ↓
Binary Search on Answer

Neither?
        ↓
Do not force binary search.
```

------------------------------------------------------------------------

# 77. MINI PRACTICE --- PROBLEM 1

## Find First Element \>= Target

Input:

``` text
arr = [1,2,4,4,7,9]
target = 5
```

Expected:

``` text
index = 4
```

### Hint

Think:

``` text
lower bound
```

When:

``` text
arr[mid] >= target
```

the current position may be an answer.

Save it implicitly by moving:

``` text
right = mid
```

------------------------------------------------------------------------

# 78. MINI PRACTICE --- PROBLEM 2

## Find Minimum in a Rotated Sorted Array

Input:

``` text
[4,5,6,7,0,1,2]
```

Answer:

``` text
0
```

### Hint

Compare:

``` text
arr[mid]
arr[right]
```

If:

``` text
arr[mid] > arr[right]
```

the minimum lies to the right.

Otherwise, it is at `mid` or to the left.

------------------------------------------------------------------------

# 79. FULL PRACTICE --- STANDARD BINARY SEARCH

## Problem

Search:

``` text
target = 23
```

in:

``` text
[2,5,8,12,16,23,38]
```

------------------------------------------------------------------------

## Input

``` text
arr = [2,5,8,12,16,23,38]
target = 23
```

------------------------------------------------------------------------

## Observation

The array is sorted.

Therefore:

``` text
Binary Search
```

------------------------------------------------------------------------

## Dry Run

``` text
left = 0
right = 6
mid = 3
arr[mid] = 12
```

Since:

``` text
12 < 23
```

move:

``` text
left = 4
```

Now:

``` text
left = 4
right = 6
mid = 5
arr[mid] = 23
```

Found.

Answer:

``` text
5
```

------------------------------------------------------------------------

## Code

``` java
public static int search(int[] nums, int target) {

    int left = 0;
    int right = nums.length - 1;

    while (left <= right) {

        int mid = left + (right - left) / 2;

        if (nums[mid] == target) {
            return mid;
        }

        if (nums[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }

    return -1;
}
```

------------------------------------------------------------------------

## Complexity

``` text
Time: O(log n)
Space: O(1)
```

------------------------------------------------------------------------

# 80. FULL PRACTICE --- FIRST AND LAST POSITION

Input:

``` text
nums = [1,2,2,2,4,5]
target = 2
```

Expected:

``` text
[1,3]
```

Approach:

``` text
First occurrence
+
Last occurrence
```

Code:

``` java
public static int[] searchRange(int[] nums, int target) {

    int first = firstOccurrence(nums, target);
    int last = lastOccurrence(nums, target);

    return new int[]{first, last};
}
```

Complexity:

``` text
O(log n)
```

because each boundary search is `O(log n)`.

------------------------------------------------------------------------

# 81. FULL PRACTICE --- BINARY SEARCH ON ANSWER

## Problem

``` text
piles = [3,6,7,11]
h = 8
```

Find minimum speed.

### Search space

``` text
left = 1
right = 11
```

### Feasibility

``` text
canFinish(speed)
```

If speed is sufficient:

``` text
true
```

Otherwise:

``` text
false
```

Pattern:

``` text
F F F T T T
```

Find the first true.

------------------------------------------------------------------------

## Core Code

``` java
public static int minEatingSpeed(int[] piles, int h) {

    int left = 1;
    int right = 0;

    for (int pile : piles) {
        right = Math.max(right, pile);
    }

    while (left < right) {

        int mid = left + (right - left) / 2;

        if (canFinish(piles, h, mid)) {
            right = mid;
        } else {
            left = mid + 1;
        }
    }

    return left;
}

private static boolean canFinish(
        int[] piles,
        int h,
        int speed) {

    long hours = 0;

    for (int pile : piles) {

        hours += (pile + (long) speed - 1) / speed;

        if (hours > h) {
            return false;
        }
    }

    return true;
}
```

------------------------------------------------------------------------

# 82. PATTERN COMPARISON

  Problem Clue              Pattern
  ------------------------- -------------------------
  Arrange values            Sorting
  Need ordered values       Sorting
  Sorted + exact search     Binary Search
  First occurrence          Boundary Binary Search
  Last occurrence           Boundary Binary Search
  First `>= target`         Lower Bound
  First `> target`          Upper Bound
  Insertion position        Lower Bound
  Rotated sorted array      Modified Binary Search
  Minimum feasible answer   Binary Search on Answer
  Sorted + pair             Sorting + Two Pointers

------------------------------------------------------------------------

# 83. PRACTICE PROBLEMS

## EASY

### 1. Binary Search

Platform:

LeetCode

Difficulty:

Easy

Pattern:

Binary Search

What to notice:

This is the standard exact-search template.

Expected:

``` text
O(log n) time
O(1) extra space
```

Practice:

https://leetcode.com/problems/binary-search/

------------------------------------------------------------------------

### 2. Search Insert Position

Platform:

LeetCode

Difficulty:

Easy

Pattern:

Lower Bound

What to notice:

Find the first index where:

``` text
nums[i] >= target
```

Practice:

https://leetcode.com/problems/search-insert-position/

------------------------------------------------------------------------

### 3. First Bad Version

Platform:

LeetCode

Difficulty:

Easy

Pattern:

Boundary Binary Search

What to notice:

The versions have a monotonic structure:

``` text
false false false true true
```

Practice:

https://leetcode.com/problems/first-bad-version/

------------------------------------------------------------------------

### 4. Find Smallest Letter Greater Than Target

Platform:

LeetCode

Difficulty:

Easy

Pattern:

Upper-bound-style binary search

What to notice:

Find the first character strictly greater than the target, with
wrap-around.

Practice:

https://leetcode.com/problems/find-smallest-letter-greater-than-target/

------------------------------------------------------------------------

## MEDIUM

### 5. Search in Rotated Sorted Array

Platform:

LeetCode

Difficulty:

Medium

Pattern:

Modified Binary Search

What to notice:

At least one side is sorted.

Practice:

https://leetcode.com/problems/search-in-rotated-sorted-array/

------------------------------------------------------------------------

### 6. Find First and Last Position of Element in Sorted Array

Platform:

LeetCode

Difficulty:

Medium

Pattern:

Boundary Binary Search

What to notice:

Find both boundaries instead of returning the first match.

Practice:

https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/

------------------------------------------------------------------------

### 7. Find Minimum in Rotated Sorted Array

Platform:

LeetCode

Difficulty:

Medium

Pattern:

Binary Search

What to notice:

Compare `mid` with the right boundary to locate the minimum.

Practice:

https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/

------------------------------------------------------------------------

### 8. Koko Eating Bananas

Platform:

LeetCode

Difficulty:

Medium

Pattern:

Binary Search on Answer

What to notice:

If speed `k` works, every larger speed works.

Practice:

https://leetcode.com/problems/koko-eating-bananas/

------------------------------------------------------------------------

## HARD / CHALLENGE

### 9. Median of Two Sorted Arrays

Platform:

LeetCode

Difficulty:

Hard

Pattern:

Advanced Binary Search / Partition

What to notice:

Binary search is applied to a partition rather than simply looking for a
value.

Practice:

https://leetcode.com/problems/median-of-two-sorted-arrays/

------------------------------------------------------------------------

### 10. Split Array Largest Sum

Platform:

LeetCode

Difficulty:

Hard

Pattern:

Binary Search on Answer + Greedy Feasibility

What to notice:

Binary-search the maximum allowed subarray sum.

Practice:

https://leetcode.com/problems/split-array-largest-sum/

------------------------------------------------------------------------

# 84. PRACTICE ORDER

Recommended order:

``` text
1. Binary Search
       ↓
2. Search Insert Position
       ↓
3. First Bad Version
       ↓
4. Find Smallest Letter Greater Than Target
       ↓
5. First and Last Position
       ↓
6. Find Minimum in Rotated Sorted Array
       ↓
7. Search in Rotated Sorted Array
       ↓
8. Koko Eating Bananas
       ↓
9. Split Array Largest Sum
       ↓
10. Median of Two Sorted Arrays
```

Do not jump directly to the hard problems.

First master:

``` text
standard binary search
        ↓
boundary search
        ↓
rotated search
        ↓
binary search on answer
```

------------------------------------------------------------------------

# 85. DAILY TEST --- 10 QUESTIONS

## Q1

What is the typical complexity of efficient comparison sorting?

A. `O(1)`

B. `O(log n)`

C. `O(n log n)`

D. `O(n³)`

------------------------------------------------------------------------

## Q2

Which sorting algorithm repeatedly compares neighboring elements?

A. Selection Sort

B. Bubble Sort

C. Merge Sort

D. Quick Sort

------------------------------------------------------------------------

## Q3

Which algorithm repeatedly selects the minimum remaining element?

A. Bubble Sort

B. Selection Sort

C. Merge Sort

D. Binary Search

------------------------------------------------------------------------

## Q4

Which simple sorting algorithm can perform well on nearly sorted data?

A. Insertion Sort

B. Selection Sort

C. Binary Search

D. DFS

------------------------------------------------------------------------

## Q5

Standard binary search requires:

A. Random data

B. Sorted/orderable search space

C. A HashMap

D. A linked list

------------------------------------------------------------------------

## Q6

What is standard binary search complexity?

A. `O(n²)`

B. `O(n)`

C. `O(log n)`

D. `O(n log n)`

------------------------------------------------------------------------

## Q7

Lower bound means:

A. First value `> target`

B. First value `>= target`

C. Last value `< target`

D. Minimum value

------------------------------------------------------------------------

## Q8

When finding the first occurrence and `arr[mid] == target`, you should
generally:

A. Return immediately

B. Save `mid` and search left

C. Search right only

D. Sort again

------------------------------------------------------------------------

## Q9

Binary Search on Answer is useful when:

A. Candidate feasibility is monotonic

B. The array is random

C. The input contains only negative values

D. There are no constraints

------------------------------------------------------------------------

## Q10

A feasibility pattern such as:

``` text
false false false true true true
```

is an example of:

A. Hashing

B. Monotonicity

C. Recursion

D. Prefix sum

------------------------------------------------------------------------

# 86. ANSWER KEY

``` text
Q1 → C
Q2 → B
Q3 → B
Q4 → A
Q5 → B
Q6 → C
Q7 → B
Q8 → B
Q9 → A
Q10 → B
```

------------------------------------------------------------------------

# 87. PATTERN RECOGNITION TEST

Identify the pattern **before writing code**.

## Problem A

``` text
Find a number in a sorted array.
```

Pattern:

``` text
____________________
```

------------------------------------------------------------------------

## Problem B

``` text
Find the first index where value >= target.
```

Pattern:

``` text
____________________
```

------------------------------------------------------------------------

## Problem C

``` text
Find minimum speed so all work finishes within a deadline.
```

Pattern:

``` text
____________________
```

------------------------------------------------------------------------

## Problem D

``` text
A sorted array was rotated.
Find a target.
```

Pattern:

``` text
____________________
```

------------------------------------------------------------------------

## Problem E

``` text
Sort an integer array in Java.
No custom sorting algorithm is requested.
```

Pattern:

``` text
____________________
```

------------------------------------------------------------------------

## Answers

``` text
A → Binary Search

B → Lower Bound / Boundary Binary Search

C → Binary Search on Answer

D → Modified Binary Search

E → Arrays.sort()
```

------------------------------------------------------------------------

# 88. HOMEWORK

## Homework 1

Implement from memory:

``` text
Bubble Sort
Selection Sort
Insertion Sort
Merge Sort
Quick Sort
```

Focus on understanding the algorithm rather than blindly memorizing
syntax.

------------------------------------------------------------------------

## Homework 2

Implement standard:

``` text
Binary Search
```

without looking at the template.

------------------------------------------------------------------------

## Homework 3

Implement:

``` text
First Occurrence
Last Occurrence
```

------------------------------------------------------------------------

## Homework 4

Implement:

``` text
Lower Bound
Upper Bound
```

Then explain:

> How can lower bound and upper bound count occurrences?

------------------------------------------------------------------------

## Homework 5

Solve:

``` text
Koko Eating Bananas
```

Before coding, write:

``` text
minimum answer =
maximum answer =
isPossible(mid) =
monotonic direction =
```

------------------------------------------------------------------------

# 89. QUICK REVISION

## Sorting

``` text
Bubble
→ swap adjacent elements

Selection
→ select minimum

Insertion
→ insert into sorted prefix

Merge
→ divide + merge

Quick
→ pivot + partition
```

------------------------------------------------------------------------

## Binary Search

``` text
Sorted search space
        ↓
left + right
        ↓
mid
        ↓
discard half
        ↓
O(log n)
```

------------------------------------------------------------------------

## First Occurrence

``` text
found
↓
save
↓
go left
```

------------------------------------------------------------------------

## Last Occurrence

``` text
found
↓
save
↓
go right
```

------------------------------------------------------------------------

## Lower Bound

``` text
first >= target
```

------------------------------------------------------------------------

## Upper Bound

``` text
first > target
```

------------------------------------------------------------------------

## Binary Search on Answer

``` text
candidate
    ↓
isPossible?
    ↓
F F F T T T
    ↓
find boundary
```

------------------------------------------------------------------------

# 90. MUST-MEMORIZE JAVA TEMPLATES

## Standard Binary Search

``` java
int left = 0;
int right = arr.length - 1;

while (left <= right) {

    int mid = left + (right - left) / 2;

    if (arr[mid] == target) {
        return mid;
    }

    if (arr[mid] < target) {
        left = mid + 1;
    } else {
        right = mid - 1;
    }
}

return -1;
```

------------------------------------------------------------------------

## Lower Bound

``` java
int left = 0;
int right = arr.length;

while (left < right) {

    int mid = left + (right - left) / 2;

    if (arr[mid] >= target) {
        right = mid;
    } else {
        left = mid + 1;
    }
}

return left;
```

------------------------------------------------------------------------

## Upper Bound

``` java
int left = 0;
int right = arr.length;

while (left < right) {

    int mid = left + (right - left) / 2;

    if (arr[mid] > target) {
        right = mid;
    } else {
        left = mid + 1;
    }
}

return left;
```

------------------------------------------------------------------------

## Binary Search on Answer

``` java
long left = minAnswer;
long right = maxAnswer;

while (left < right) {

    long mid = left + (right - left) / 2;

    if (isPossible(mid)) {
        right = mid;
    } else {
        left = mid + 1;
    }
}

return left;
```

------------------------------------------------------------------------

# 91. INTERVIEW CHEAT SHEET

If the interviewer says:

### "The array is sorted."

Think:

``` text
Binary Search
Two Pointers
```

------------------------------------------------------------------------

### "Find first/last position."

Think:

``` text
Boundary Binary Search
```

------------------------------------------------------------------------

### "Find the first value \>= target."

Think:

``` text
Lower Bound
```

------------------------------------------------------------------------

### "Find the first value \> target."

Think:

``` text
Upper Bound
```

------------------------------------------------------------------------

### "Find minimum possible X."

Ask:

``` text
Is feasibility monotonic?
```

If yes:

``` text
Binary Search on Answer
```

------------------------------------------------------------------------

### "Sort and then solve."

Ask:

``` text
What does sorting unlock?
```

Possible answers:

``` text
Binary Search
Two Pointers
Greedy
Grouping
Intervals
```

------------------------------------------------------------------------

# 92. GOLDEN RULES

Memorize these:

> **Sorted search space → Think Binary Search**

> **Each step halves the search space → O(log n)**

> **First occurrence → save + go left**

> **Last occurrence → save + go right**

> **Lower Bound → first \>= target**

> **Upper Bound → first \> target**

> **Minimum possible answer + monotonic feasibility → Binary Search on
> Answer**

> **Sorting can be preprocessing, not the final answer**

> **If library sorting is allowed, `Arrays.sort()` is usually the
> practical Java choice**

------------------------------------------------------------------------

# 93. DAY COMPLETION CHECKLIST

``` text
☐ I understand why sorting is useful
☐ I understand stable sorting
☐ I understand in-place sorting
☐ I understand Bubble Sort
☐ I can implement Bubble Sort
☐ I understand Selection Sort
☐ I can implement Selection Sort
☐ I understand Insertion Sort
☐ I can implement Insertion Sort
☐ I understand Merge Sort
☐ I understand divide and conquer
☐ I understand Quick Sort
☐ I understand pivot and partition
☐ I know sorting complexities
☐ I know when to use Arrays.sort()
☐ I understand binary search
☐ I can implement standard binary search
☐ I understand the binary-search invariant
☐ I can find first occurrence
☐ I can find last occurrence
☐ I understand lower bound
☐ I understand upper bound
☐ I understand insertion position
☐ I understand rotated sorted array search
☐ I understand binary search on answer
☐ I understand monotonic feasibility
☐ I completed the daily test
☐ I completed the pattern recognition test
☐ I completed the homework
☐ I solved the Easy practice problems
☐ I attempted the Medium problems
```

------------------------------------------------------------------------

# 94. DAY 7 MASTER SUMMARY

The most important transition today is:

``` text
Sorting
   ↓
Create useful order
   ↓
Unlock efficient patterns
```

and:

``` text
Binary Search
   ↓
Use order / monotonicity
   ↓
Discard half
   ↓
O(log n)
```

Your mental model should be:

``` text
Question
   ↓
Is there useful order?
   ↓
YES
   ├── Exact search?
   │       ↓
   │   Binary Search
   │
   ├── Boundary?
   │       ↓
   │   Lower / Upper Bound
   │
   ├── Pair relationship?
   │       ↓
   │   Sorting + Two Pointers
   │
   └── Minimum / maximum feasible answer?
           ↓
       Binary Search on Answer
```

The goal is not to memorize five sorting algorithms mechanically.

The goal is to recognize:

> **What structure does sorting create, and what can I do faster because
> of that structure?**

------------------------------------------------------------------------

# 95. NAVIGATION

**Previous:** [Day 6 --- Two Pointers + Sliding
Window](Day-06-Two-Pointers-Sliding-Window.md)

**Next:** [Day 8 --- Recursion +
Backtracking](Day-08-Recursion-Backtracking.md)

**Course:** Java DSA Placement Preparation

------------------------------------------------------------------------

# 🎯 DAY 7 COMPLETE

You have now learned:

``` text
SORTING
    ↓
Bubble
Selection
Insertion
Merge
Quick
Arrays.sort()

BINARY SEARCH
    ↓
Exact search
First occurrence
Last occurrence
Lower bound
Upper bound
Insertion position
Rotated array
Binary search on answer

PATTERN RECOGNITION
    ↓
Sorted?
Monotonic?
Boundary?
Minimum possible answer?
        ↓
Binary Search
```

**Do not move to Day 8 until you can identify the binary-search pattern
before writing the code.**
