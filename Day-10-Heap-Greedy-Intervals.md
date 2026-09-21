# Day 10 --- Heap + Greedy + Intervals

> **Placement-focused Java DSA course \| Beginner + Revision**

------------------------------------------------------------------------

# 1. Today's Goal

By the end of Day 10, you should be able to:

-   Understand what a heap is and why it is useful.
-   Distinguish a min-heap from a max-heap.
-   Use Java `PriorityQueue`.
-   Find the kth largest/smallest element efficiently.
-   Solve top-k frequency style problems.
-   Understand heap construction and heap sort conceptually.
-   Recognize when a priority queue is the correct pattern.
-   Understand greedy algorithms and why local choices sometimes lead to
    a global optimum.
-   Know how to test whether a greedy idea is actually valid.
-   Solve interval overlap, merge, scheduling, and insertion problems.
-   Recognize interval patterns from problem wording.
-   Compare brute force with heap/greedy/interval solutions.
-   Explain time and space complexity in interviews.

### Today's highest-priority patterns

``` text
Heap / PriorityQueue
Greedy choice
Sort by endpoint
Sort by start
Merge intervals
Overlap detection
Meeting-room scheduling
Top K
```

------------------------------------------------------------------------

# 2. Prerequisites

You should already know:

-   Java basics
-   arrays
-   strings
-   hashing
-   sorting
-   binary search
-   linked lists
-   stack and queue
-   basic recursion

Previous: - [Day 9 --- Linked List + Stack +
Queue](Day-09-Linked-List-Stack-Queue.md)

Next: - [Day 11 --- Trees](Day-11-Trees.md)

------------------------------------------------------------------------

# 3. Why Heap + Greedy + Intervals Together?

These topics look different, but they frequently appear together in
coding assessments.

For example:

``` text
Given many intervals representing meetings,
find the minimum rooms needed.
```

You may need:

``` text
sort intervals
+
priority queue
```

Another example:

``` text
Given many jobs with deadlines,
choose jobs to maximize profit.
```

You may need:

``` text
sort
+
greedy
+
heap
```

The important skill is not memorizing isolated algorithms.

The goal is:

``` text
Problem
   ↓
Recognize structure
   ↓
Choose pattern
   ↓
Optimize
   ↓
Code
   ↓
Analyze complexity
```

------------------------------------------------------------------------

# PART A --- HEAP

# 4. What Is a Heap?

## 🧑‍🎓 Beginner Explanation

A heap is a special tree-based data structure that lets us quickly
access the smallest or largest element.

A **min-heap** keeps the smallest element at the top.

A **max-heap** keeps the largest element at the top.

Conceptually:

``` text
Min Heap

        1
       / \
      3   5
     / \
    7   8
```

The exact shape is maintained as a complete binary tree.

------------------------------------------------------------------------

## ⚡ 30-Second Revision

``` text
Min Heap → smallest at top
Max Heap → largest at top
Java      → PriorityQueue
```

------------------------------------------------------------------------

# 5. Heap Terminology

### Root

Top element.

### Parent

A node with children.

### Child

Node below a parent.

### Complete Binary Tree

Every level is full except possibly the last, and the last level is
filled from left to right.

### Heap Property

Min-heap:

``` text
parent <= children
```

Max-heap:

``` text
parent >= children
```

Important:

> A heap is **not fully sorted**.

Only the required extreme is guaranteed at the root.

------------------------------------------------------------------------

# 6. Min-Heap

Example:

``` text
        2
       / \
      4   3
     / \
    8   7
```

The minimum is always:

``` text
root = 2
```

Java:

``` java
PriorityQueue<Integer> minHeap = new PriorityQueue<>();
```

Add:

``` java
minHeap.offer(10);
minHeap.offer(3);
minHeap.offer(7);
```

Peek:

``` java
minHeap.peek();
```

Remove minimum:

``` java
minHeap.poll();
```

------------------------------------------------------------------------

# 7. Max-Heap in Java

Java's default `PriorityQueue` is a min-heap.

For a max-heap:

``` java
PriorityQueue<Integer> maxHeap =
        new PriorityQueue<>(Collections.reverseOrder());
```

Or:

``` java
PriorityQueue<Integer> maxHeap =
        new PriorityQueue<>((a, b) -> b - a);
```

For safe comparison with large integers, prefer:

``` java
PriorityQueue<Integer> maxHeap =
        new PriorityQueue<>((a, b) -> Integer.compare(b, a));
```

------------------------------------------------------------------------

# 8. PriorityQueue Operations

  Operation                               Complexity
  ------------------------------ -------------------
  `peek()`                                      O(1)
  `offer()`                                 O(log n)
  `poll()`                                  O(log n)
  build heap from all elements     O(n) with heapify
  search arbitrary value                        O(n)

Important:

``` text
peek ≠ sorted traversal
```

You only get the highest-priority element efficiently.

------------------------------------------------------------------------

# 9. Heap Visualization

Suppose:

``` text
insert: 10
insert: 4
insert: 7
insert: 1
```

Min-heap may look like:

``` text
        1
       / \
      4   7
     /
    10
```

The exact internal arrangement can vary while satisfying heap rules.

------------------------------------------------------------------------

# 10. Heap vs Sorted Array

Suppose you need the minimum repeatedly.

### Sorted array

``` text
[1,2,3,4,5]
```

Finding minimum is easy, but maintaining sorted order after insertion
can be expensive.

### Heap

``` text
        1
       / \
      2   3
```

You can repeatedly:

``` text
peek minimum
poll minimum
insert new item
```

without fully sorting everything.

### Pattern

If the problem repeatedly asks:

``` text
minimum
maximum
smallest remaining
largest remaining
next event
next job
```

think:

``` text
PriorityQueue
```

------------------------------------------------------------------------

# 11. Kth Largest Element

Example:

``` text
nums = [3,2,1,5,6,4]
k = 2
```

Answer:

``` text
5
```

------------------------------------------------------------------------

## Brute Force

Sort descending:

``` text
[6,5,4,3,2,1]
```

Return index `k-1`.

Complexity:

``` text
O(n log n)
```

------------------------------------------------------------------------

## Heap Optimization

Maintain a **min-heap of size k**.

Why?

For:

``` text
k = 2
```

we only need to remember the two largest values seen so far.

``` java
int findKthLargest(int[] nums, int k) {

    PriorityQueue<Integer> heap = new PriorityQueue<>();

    for (int num : nums) {

        heap.offer(num);

        if (heap.size() > k) {
            heap.poll();
        }
    }

    return heap.peek();
}
```

Complexity:

``` text
Time = O(n log k)
Space = O(k)
```

------------------------------------------------------------------------

# 12. Why Min-Heap for Kth Largest?

This is a common interview confusion.

Suppose:

``` text
k = 3
```

We maintain:

``` text
three largest elements
```

The smallest among those three is the answer.

Therefore:

``` text
min-heap
```

keeps the weakest of the top-k candidates at the root.

When a new number arrives:

``` text
add it
if size > k:
    remove smallest
```

------------------------------------------------------------------------

# 13. Kth Smallest

For kth smallest, reverse the idea.

Maintain a **max-heap of size k**.

``` java
int kthSmallest(int[] nums, int k) {

    PriorityQueue<Integer> heap =
            new PriorityQueue<>(Collections.reverseOrder());

    for (int num : nums) {

        heap.offer(num);

        if (heap.size() > k) {
            heap.poll();
        }
    }

    return heap.peek();
}
```

Complexity:

``` text
O(n log k)
```

------------------------------------------------------------------------

# 14. Top K Pattern

A very important general pattern:

``` text
Need K largest
→ min-heap size K

Need K smallest
→ max-heap size K
```

Why?

Because the heap stores only the useful candidates.

This prevents:

``` text
sorting all n elements
```

when only k elements matter.

------------------------------------------------------------------------

# 15. Top K Frequent Elements

Suppose:

``` text
[1,1,1,2,2,3]
```

k = 2

Answer:

``` text
[1,2]
```

### Step 1

Count frequency.

``` text
1 -> 3
2 -> 2
3 -> 1
```

### Step 2

Use a min-heap ordered by frequency.

``` java
PriorityQueue<int[]> heap =
        new PriorityQueue<>((a, b) -> Integer.compare(a[1], b[1]));
```

Then keep size k.

------------------------------------------------------------------------

# 16. Top K Frequent Code

``` java
int[] topKFrequent(int[] nums, int k) {

    HashMap<Integer, Integer> freq = new HashMap<>();

    for (int num : nums) {
        freq.put(num, freq.getOrDefault(num, 0) + 1);
    }

    PriorityQueue<int[]> heap =
            new PriorityQueue<>(
                    (a, b) -> Integer.compare(a[1], b[1])
            );

    for (Map.Entry<Integer, Integer> entry : freq.entrySet()) {

        heap.offer(new int[]{entry.getKey(), entry.getValue()});

        if (heap.size() > k) {
            heap.poll();
        }
    }

    int[] answer = new int[k];

    for (int i = k - 1; i >= 0; i--) {
        answer[i] = heap.poll()[0];
    }

    return answer;
}
```

Complexity:

``` text
Counting = O(n)
Heap = O(m log k)
```

where m is number of distinct values.

Overall:

``` text
O(n + m log k)
```

------------------------------------------------------------------------

# 17. Heap of Objects / Pairs in Java

Java has no built-in generic pair in basic coding environments.

Common approach:

``` java
PriorityQueue<int[]> heap =
    new PriorityQueue<>(
        (a, b) -> Integer.compare(a[1], b[1])
    );
```

Here:

``` text
a[0] = value
a[1] = frequency
```

Be careful to document what each index means.

------------------------------------------------------------------------

# 18. K Closest Points

Given points:

``` text
[x,y]
```

find k points closest to origin.

Distance:

``` text
x² + y²
```

No square root is needed because square root preserves ordering for
nonnegative values.

A max-heap of size k can keep the k closest points.

``` java
PriorityQueue<int[]> heap =
        new PriorityQueue<>(
            (a, b) -> Integer.compare(
                distance(b),
                distance(a)
            )
        );
```

Helper:

``` java
int distance(int[] point) {
    return point[0] * point[0] + point[1] * point[1];
}
```

For very large coordinates, use `long` for the squared distance.

------------------------------------------------------------------------

# 19. Merge K Sorted Lists --- Heap Idea

Suppose:

``` text
List 1: 1 -> 4 -> 7
List 2: 2 -> 5 -> 8
List 3: 3 -> 6 -> 9
```

At any point, only the smallest current head of each list matters.

Put the current head from each list into a min-heap.

Then:

``` text
poll smallest
add its next node
repeat
```

If there are k lists and N total nodes:

``` text
Time = O(N log k)
Space = O(k)
```

This is the central **heap + k streams** pattern.

------------------------------------------------------------------------

# 20. Two Heaps Pattern

Sometimes one heap is not enough.

Example:

``` text
Find median of a stream
```

Use:

``` text
max-heap → smaller half
min-heap → larger half
```

Visualization:

``` text
smaller half        larger half

maxHeap             minHeap
   4                   7
  / \                 / \
 2   3               8   9
```

Keep sizes balanced.

Median:

``` text
if equal size:
    average of roots
else:
    root of larger heap
```

This is an advanced pattern worth recognizing.

------------------------------------------------------------------------

# 21. Heapify Concept

Heapify transforms an array into a heap.

For a heap represented by an array:

``` text
parent = (i - 1) / 2
left   = 2*i + 1
right  = 2*i + 2
```

These formulas are extremely important.

------------------------------------------------------------------------

# 22. Heap Array Representation

Example:

``` text
        1
       / \
      3   5
     / \
    7   8
```

Array:

``` text
[1,3,5,7,8]
```

For index `i`:

``` text
parent = (i - 1) / 2
left   = 2*i + 1
right  = 2*i + 2
```

------------------------------------------------------------------------

# 23. Heap Sort

Heap sort:

1.  Build heap.
2.  Repeatedly remove extreme element.
3.  Place it in final position.

Complexity:

``` text
Time = O(n log n)
Space = O(1) auxiliary for in-place implementation
```

For placements, you usually need to understand the idea and complexity
before implementing heap sort from scratch.

------------------------------------------------------------------------

# PART B --- GREEDY

# 24. What Is Greedy?

## 🧑‍🎓 Beginner Explanation

A greedy algorithm makes the best-looking choice **right now**.

It does not necessarily explore every future possibility.

Example:

``` text
You have activities with start/end times.
Choose as many non-overlapping activities as possible.
```

A powerful greedy choice is:

``` text
Choose the activity that finishes earliest.
```

Why?

Because it leaves the maximum remaining time for future activities.

------------------------------------------------------------------------

## ⚡ 30-Second Revision

``` text
Greedy = choose a locally optimal option
         hoping it leads to a global optimum.
```

But:

> You must prove or understand why the greedy choice is safe.

------------------------------------------------------------------------

# 25. Greedy vs Brute Force

Suppose there are many possible choices.

Brute force:

``` text
try all combinations
```

Could be exponential.

Greedy:

``` text
sort / choose best local option / continue
```

Can be:

``` text
O(n log n)
```

But greedy is not automatically correct.

------------------------------------------------------------------------

# 26. When Should You Suspect Greedy?

Look for clues:

-   maximize number of activities;
-   minimize number of resources;
-   choose earliest finishing;
-   choose smallest/largest available;
-   scheduling;
-   intervals;
-   deadlines;
-   locally optimal repeated decisions;
-   "minimum number of..."
-   "maximum number of non-overlapping..."

But clues alone do not prove greedy correctness.

------------------------------------------------------------------------

# 27. Activity Selection

Given:

``` text
start = [1,3,0,5,8,5]
end   = [2,4,6,7,9,9]
```

Goal:

``` text
maximum number of non-overlapping activities
```

### Greedy rule

Sort by ending time.

Then repeatedly choose the first activity whose start is at least the
previous selected end.

------------------------------------------------------------------------

# 28. Activity Selection Code

``` java
int maxActivities(int[][] activities) {

    Arrays.sort(
        activities,
        (a, b) -> Integer.compare(a[1], b[1])
    );

    int count = 0;
    int lastEnd = Integer.MIN_VALUE;

    for (int[] activity : activities) {

        if (activity[0] >= lastEnd) {
            count++;
            lastEnd = activity[1];
        }
    }

    return count;
}
```

Complexity:

``` text
Sorting = O(n log n)
Scan = O(n)

Total = O(n log n)
```

------------------------------------------------------------------------

# 29. Why Earliest Finish?

Suppose:

``` text
A finishes at 4
B finishes at 6
```

Choosing A leaves more room for future activities.

This is an **exchange argument** idea:

If an optimal solution chooses another compatible activity that finishes
later, we can replace it with the earlier-finishing activity without
reducing the number of activities we can schedule afterward.

You do not need a formal proof for every placement question, but you
should understand the reasoning.

------------------------------------------------------------------------

# 30. Greedy Warning

This is crucial:

``` text
Greedy works for some optimization problems,
not all.
```

Example:

``` text
Coin values = [1,3,4]
target = 6
```

Greedy picks:

``` text
4 + 1 + 1 = 3 coins
```

But optimal is:

``` text
3 + 3 = 2 coins
```

So:

``` text
"take the largest coin first"
```

is not universally valid.

When greedy fails, dynamic programming may be needed.

------------------------------------------------------------------------

# 31. Fractional Knapsack

Items have:

``` text
value
weight
```

You may take fractions of items.

Greedy rule:

``` text
highest value / weight ratio first
```

Because fractions are allowed.

This is different from 0/1 knapsack, where you either take an item or do
not.

------------------------------------------------------------------------

# 32. Interval Scheduling

This is where greedy and intervals meet.

Typical questions:

``` text
maximum non-overlapping meetings
minimum rooms
remove overlapping intervals
merge intervals
insert interval
```

First ask:

``` text
Are intervals being merged?
Are we counting overlaps?
Are we selecting a maximum number?
Are we assigning resources?
```

That determines the pattern.

------------------------------------------------------------------------

# PART C --- INTERVALS

# 33. What Is an Interval?

An interval is usually:

``` text
[start, end]
```

Example:

``` text
[2,5]
```

means a range beginning at 2 and ending at 5.

Multiple intervals:

``` text
[1,3]
[2,6]
[8,10]
```

------------------------------------------------------------------------

# 34. Visualizing Overlap

``` text
A: 1 ---- 5
B:    3 ---- 7

overlap:
      3 -- 5
```

Two intervals overlap when:

``` text
startB <= endA
```

assuming they are ordered appropriately.

More generally, `[a,b]` and `[c,d]` overlap when:

``` text
max(a,c) <= min(b,d)
```

for closed intervals.

------------------------------------------------------------------------

# 35. Interval Pattern 1 --- Merge Intervals

Input:

``` text
[[1,3],[2,6],[8,10],[9,12]]
```

Output:

``` text
[[1,6],[8,12]]
```

### Key observation

Sort by start time.

Then compare current interval with the last merged interval.

------------------------------------------------------------------------

# 36. Merge Intervals Code

``` java
int[][] merge(int[][] intervals) {

    if (intervals.length <= 1) {
        return intervals;
    }

    Arrays.sort(
        intervals,
        (a, b) -> Integer.compare(a[0], b[0])
    );

    List<int[]> result = new ArrayList<>();

    int start = intervals[0][0];
    int end = intervals[0][1];

    for (int i = 1; i < intervals.length; i++) {

        int currentStart = intervals[i][0];
        int currentEnd = intervals[i][1];

        if (currentStart <= end) {
            end = Math.max(end, currentEnd);
        } else {
            result.add(new int[]{start, end});
            start = currentStart;
            end = currentEnd;
        }
    }

    result.add(new int[]{start, end});

    return result.toArray(new int[result.size()][]);
}
```

Complexity:

``` text
Time = O(n log n)
Space = O(n)
```

The sorting dominates.

------------------------------------------------------------------------

# 37. Merge Intervals Dry Run

Input:

``` text
[1,3]
[2,6]
[8,10]
[9,12]
```

Sort by start:

``` text
[1,3]
[2,6]
[8,10]
[9,12]
```

Start:

``` text
current = [1,3]
```

Next:

``` text
[2,6]
```

Since:

``` text
2 <= 3
```

merge:

``` text
[1,6]
```

Next:

``` text
[8,10]
```

Since:

``` text
8 > 6
```

save `[1,6]`.

Then merge `[8,10]` and `[9,12]`:

``` text
[8,12]
```

Answer:

``` text
[[1,6],[8,12]]
```

------------------------------------------------------------------------

# 38. Interval Pattern 2 --- Insert Interval

Suppose existing intervals:

``` text
[1,3]
[6,9]
```

Insert:

``` text
[2,5]
```

Result:

``` text
[1,5]
[6,9]
```

Three phases:

``` text
1. intervals completely before new interval
2. merge overlapping intervals
3. intervals completely after
```

------------------------------------------------------------------------

# 39. Insert Interval Code

``` java
int[][] insert(int[][] intervals, int[] newInterval) {

    List<int[]> result = new ArrayList<>();

    int i = 0;
    int n = intervals.length;

    while (i < n && intervals[i][1] < newInterval[0]) {
        result.add(intervals[i]);
        i++;
    }

    while (i < n && intervals[i][0] <= newInterval[1]) {
        newInterval[0] =
                Math.min(newInterval[0], intervals[i][0]);

        newInterval[1] =
                Math.max(newInterval[1], intervals[i][1]);

        i++;
    }

    result.add(newInterval);

    while (i < n) {
        result.add(intervals[i]);
        i++;
    }

    return result.toArray(new int[result.size()][]);
}
```

Complexity:

``` text
Time = O(n)
Space = O(n)
```

assuming the input intervals are already sorted and non-overlapping.

------------------------------------------------------------------------

# 40. Interval Pattern 3 --- Non-Overlapping Intervals

Problem idea:

``` text
Remove the minimum number of intervals
so the rest do not overlap.
```

Equivalent:

``` text
Keep the maximum number of non-overlapping intervals.
```

This becomes activity selection.

Greedy rule:

``` text
sort by end
keep earliest finishing compatible interval
```

------------------------------------------------------------------------

# 41. Non-Overlapping Intervals Code

``` java
int eraseOverlapIntervals(int[][] intervals) {

    if (intervals.length <= 1) {
        return 0;
    }

    Arrays.sort(
        intervals,
        (a, b) -> Integer.compare(a[1], b[1])
    );

    int removed = 0;
    int lastEnd = intervals[0][1];

    for (int i = 1; i < intervals.length; i++) {

        if (intervals[i][0] < lastEnd) {
            removed++;
        } else {
            lastEnd = intervals[i][1];
        }
    }

    return removed;
}
```

Complexity:

``` text
O(n log n)
```

------------------------------------------------------------------------

# 42. Why Sort by End Here?

We want to keep as many intervals as possible.

An interval that ends earlier leaves more space for future intervals.

Therefore:

``` text
sort by end
```

is the greedy choice.

------------------------------------------------------------------------

# 43. Interval Pattern 4 --- Meeting Rooms

Given:

``` text
[0,30]
[5,10]
[15,20]
```

Can one person attend all meetings?

No.

Because:

``` text
[0,30]
```

overlaps with the other meetings.

A simple approach:

``` text
sort by start
compare adjacent intervals
```

------------------------------------------------------------------------

# 44. Meeting Rooms Code

``` java
boolean canAttendMeetings(int[][] intervals) {

    Arrays.sort(
        intervals,
        (a, b) -> Integer.compare(a[0], b[0])
    );

    for (int i = 1; i < intervals.length; i++) {

        if (intervals[i][0] < intervals[i - 1][1]) {
            return false;
        }
    }

    return true;
}
```

Complexity:

``` text
O(n log n)
```

------------------------------------------------------------------------

# 45. Minimum Meeting Rooms

Now ask:

``` text
How many rooms are required?
```

Example:

``` text
[0,30]
[5,10]
[15,20]
```

Answer:

``` text
2
```

because at most two meetings overlap at once.

This is a classic:

``` text
intervals + min-heap
```

problem.

------------------------------------------------------------------------

# 46. Minimum Meeting Rooms --- Heap Solution

Sort by start time.

Maintain a min-heap containing meeting end times.

For each meeting:

``` text
if earliest ending meeting ends <= current start:
    reuse that room
else:
    need a new room
```

``` java
int minMeetingRooms(int[][] intervals) {

    if (intervals.length == 0) {
        return 0;
    }

    Arrays.sort(
        intervals,
        (a, b) -> Integer.compare(a[0], b[0])
    );

    PriorityQueue<Integer> minHeap =
            new PriorityQueue<>();

    for (int[] interval : intervals) {

        if (!minHeap.isEmpty()
                && minHeap.peek() <= interval[0]) {
            minHeap.poll();
        }

        minHeap.offer(interval[1]);
    }

    return minHeap.size();
}
```

Complexity:

``` text
Sorting = O(n log n)
Heap operations = O(n log n)

Total = O(n log n)
Space = O(n)
```

------------------------------------------------------------------------

# 47. Meeting Rooms Dry Run

Intervals:

``` text
[0,30]
[5,10]
[15,20]
```

Sort:

``` text
[0,30]
[5,10]
[15,20]
```

Heap stores ending times.

After `[0,30]`:

``` text
[30]
```

After `[5,10]`:

``` text
[10,30]
```

No room free because:

``` text
10 <= 5
```

is false.

After `[15,20]`:

``` text
10 <= 15
```

so remove 10.

Heap:

``` text
[20,30]
```

Answer:

``` text
2
```

------------------------------------------------------------------------

# 48. Alternative Meeting Rooms Approach

Another solution separates:

``` text
start times
end times
```

Sort both arrays.

Then use two pointers.

This can also achieve:

``` text
O(n log n)
```

The heap approach is often easier to connect to the general
resource-allocation pattern.

------------------------------------------------------------------------

# 49. Interval Pattern Recognition

### Sort by start when:

-   merging intervals;
-   inserting intervals;
-   checking neighboring overlap;
-   processing intervals chronologically.

### Sort by end when:

-   maximizing non-overlapping intervals;
-   selecting activities;
-   minimizing removals.

### Use min-heap when:

-   tracking currently active intervals;
-   reusing earliest available resource;
-   finding minimum rooms/resources;
-   scheduling events by earliest end.

------------------------------------------------------------------------

# 50. Greedy + Heap Combination

Example:

``` text
Many tasks arrive over time.
Always process the task with the smallest deadline.
```

Possible pattern:

``` text
sort by time
+
PriorityQueue
```

Heap is often the mechanism that lets a greedy algorithm repeatedly
choose the best currently available option.

------------------------------------------------------------------------

# 51. Job Scheduling Example

Suppose jobs have:

``` text
deadline
profit
```

A common strategy for unit-time jobs:

1.  Sort jobs by descending profit.
2.  Place each job in the latest available slot before its deadline.

This is a classic greedy problem.

The important lesson is:

``` text
Sort by a useful priority.
Make the best valid choice.
Protect future opportunities.
```

------------------------------------------------------------------------

# 52. Greedy Proof Thinking

Before coding a greedy algorithm, ask:

### Question 1

What exactly is my local choice?

Example:

``` text
earliest finish
```

### Question 2

Why does this choice not hurt future choices?

Example:

``` text
earlier finish leaves more remaining time.
```

### Question 3

Can I exchange another optimal choice for mine without making the answer
worse?

If yes, you have the basis of an exchange argument.

------------------------------------------------------------------------

# 53. Greedy vs Dynamic Programming

A useful distinction:

### Greedy

``` text
Make one choice
Never reconsider it
```

### DP

``` text
Store subproblem results
Consider multiple possibilities
```

Example:

``` text
Activity Selection → greedy
0/1 Knapsack → DP
```

Do not assume every optimization problem is greedy.

------------------------------------------------------------------------

# 54. Common Beginner Mistakes

### Mistake 1 --- Thinking heap means sorted

A heap is not a sorted array.

Only the root has guaranteed priority.

------------------------------------------------------------------------

### Mistake 2 --- Wrong heap direction

Kth largest:

``` text
min-heap size k
```

Kth smallest:

``` text
max-heap size k
```

------------------------------------------------------------------------

### Mistake 3 --- Comparator overflow

Avoid:

``` java
(a, b) -> a - b
```

for general integer comparators.

Prefer:

``` java
Integer.compare(a, b)
```

or:

``` java
Integer.compare(b, a)
```

------------------------------------------------------------------------

### Mistake 4 --- Sorting by wrong interval field

Merge intervals:

``` text
sort by start
```

Activity selection:

``` text
sort by end
```

------------------------------------------------------------------------

### Mistake 5 --- Forgetting empty input

Always handle:

``` java
intervals.length == 0
```

------------------------------------------------------------------------

### Mistake 6 --- Wrong overlap condition

For closed intervals, typical overlap is:

``` text
start <= previousEnd
```

But the exact condition depends on whether touching endpoints count as
overlap in the problem.

Read the statement carefully.

------------------------------------------------------------------------

### Mistake 7 --- Assuming greedy without proof

A locally attractive choice can be globally wrong.

------------------------------------------------------------------------

# 55. Edge Cases

## Heap

-   k = 1
-   k = n
-   duplicate values
-   all values equal
-   negative numbers
-   empty input
-   k invalid according to problem constraints

## Intervals

-   no intervals
-   one interval
-   fully contained interval
-   identical intervals
-   touching endpoints
-   intervals already sorted
-   reverse-sorted input
-   all overlapping
-   no overlaps

## Greedy

-   only one choice
-   ties
-   multiple equal deadlines
-   choice that looks best locally but blocks future options

------------------------------------------------------------------------

# 56. Java DSA Notes

### Min-heap

``` java
PriorityQueue<Integer> pq = new PriorityQueue<>();
```

### Max-heap

``` java
PriorityQueue<Integer> pq =
        new PriorityQueue<>(Collections.reverseOrder());
```

### Custom comparator

``` java
PriorityQueue<int[]> pq =
        new PriorityQueue<>(
            (a, b) -> Integer.compare(a[1], b[1])
        );
```

### Interval sort

``` java
Arrays.sort(
    intervals,
    (a, b) -> Integer.compare(a[0], b[0])
);
```

or:

``` java
Arrays.sort(
    intervals,
    (a, b) -> Integer.compare(a[1], b[1])
);
```

------------------------------------------------------------------------

# 57. Complexity Cheat Sheet

  Pattern                            Typical Complexity
  -------------------------------- --------------------
  heap peek                                        O(1)
  heap insert                                  O(log n)
  heap remove                                  O(log n)
  kth largest with size-k heap               O(n log k)
  top-k frequency                        O(n + m log k)
  merge intervals                            O(n log n)
  insert interval (sorted input)                   O(n)
  activity selection                         O(n log n)
  erase overlaps                             O(n log n)
  meeting rooms                              O(n log n)

------------------------------------------------------------------------

# 58. Brute Force → Optimal

## Kth Largest

``` text
Brute:
sort all -> O(n log n)

Optimal pattern:
size-k min-heap -> O(n log k)
```

## Top K Frequent

``` text
Brute:
frequency + sort all frequencies

Optimal:
frequency + size-k heap
```

## Merge Intervals

``` text
Brute:
repeatedly compare every pair

Optimal:
sort by start + one pass
```

## Activity Selection

``` text
Brute:
try combinations

Optimal:
sort by finish + greedy
```

## Meeting Rooms

``` text
Brute:
for every meeting, count all overlaps -> O(n²)

Optimal:
sort + heap -> O(n log n)
```

------------------------------------------------------------------------

# 59. Mini Practice

## Problem 1 --- Kth Largest

Input:

``` text
[3,2,1,5,6,4]
k = 2
```

Expected:

``` text
5
```

### Hint

Maintain:

``` text
min-heap of size k
```

```{=html}
<details>
```
```{=html}
<summary>
```
Solution
```{=html}
</summary>
```
``` java
int kthLargest(int[] nums, int k) {
    PriorityQueue<Integer> heap = new PriorityQueue<>();

    for (int x : nums) {
        heap.offer(x);

        if (heap.size() > k) {
            heap.poll();
        }
    }

    return heap.peek();
}
```

Time O(n log k), space O(k).

```{=html}
</details>
```

------------------------------------------------------------------------

## Problem 2 --- Merge Intervals

Input:

``` text
[[1,3],[2,6],[8,10]]
```

Expected:

``` text
[[1,6],[8,10]]
```

### Hint

Sort by start.

```{=html}
<details>
```
```{=html}
<summary>
```
Solution idea
```{=html}
</summary>
```
Keep the current merged `[start,end]`.

If:

``` text
nextStart <= end
```

extend:

``` text
end = max(end,nextEnd)
```

Otherwise save the current interval and start a new one.

```{=html}
</details>
```

------------------------------------------------------------------------

# 60. Full Practice --- Kth Largest

### Input

``` text
[3,2,1,5,6,4]
k=2
```

### Observation

We only need the two largest values.

### Brute force

Sort:

``` text
[1,2,3,4,5,6]
```

Return 5.

Cost:

``` text
O(n log n)
```

### Better

Use min-heap size 2.

Process:

``` text
3 -> [3]
2 -> [2,3]
1 -> [2,3] after removing 1
5 -> [3,5]
6 -> [5,6]
4 -> [5,6]
```

Root:

``` text
5
```

### Code

``` java
int kthLargest(int[] nums, int k) {
    PriorityQueue<Integer> heap = new PriorityQueue<>();

    for (int x : nums) {
        heap.offer(x);

        if (heap.size() > k) {
            heap.poll();
        }
    }

    return heap.peek();
}
```

Complexity:

``` text
O(n log k) time
O(k) space
```

------------------------------------------------------------------------

# 61. Full Practice --- Merge Intervals

### Input

``` text
[[1,3],[2,6],[8,10],[9,12]]
```

### Step 1

Sort by start.

Already sorted.

### Step 2

Current:

``` text
[1,3]
```

Compare `[2,6]`.

Overlap:

``` text
2 <= 3
```

Merge:

``` text
[1,6]
```

Compare `[8,10]`.

No overlap:

``` text
8 > 6
```

Save `[1,6]`.

Now current:

``` text
[8,10]
```

Compare `[9,12]`.

Overlap.

Merge:

``` text
[8,12]
```

### Output

``` text
[[1,6],[8,12]]
```

### Complexity

``` text
O(n log n) time
O(n) output space
```

------------------------------------------------------------------------

# 62. Full Practice --- Meeting Rooms

### Input

``` text
[[0,30],[5,10],[15,20]]
```

### Observation

We need the maximum number of simultaneously active meetings.

### Approach

1.  Sort by start.
2.  Store end times in min-heap.
3.  Remove every meeting whose end is \<= current start.
4.  Add current end.
5.  Heap size = rooms needed.

### Code

``` java
int minMeetingRooms(int[][] intervals) {

    if (intervals.length == 0) {
        return 0;
    }

    Arrays.sort(
        intervals,
        (a, b) -> Integer.compare(a[0], b[0])
    );

    PriorityQueue<Integer> heap = new PriorityQueue<>();

    for (int[] interval : intervals) {

        if (!heap.isEmpty()
                && heap.peek() <= interval[0]) {
            heap.poll();
        }

        heap.offer(interval[1]);
    }

    return heap.size();
}
```

### Complexity

``` text
O(n log n) time
O(n) space
```

------------------------------------------------------------------------

# 63. Full Practice --- Activity Selection

### Goal

Maximum number of non-overlapping intervals.

### Greedy rule

Sort by end time.

### Code

``` java
int maxActivities(int[][] activities) {

    Arrays.sort(
        activities,
        (a, b) -> Integer.compare(a[1], b[1])
    );

    int count = 0;
    int lastEnd = Integer.MIN_VALUE;

    for (int[] activity : activities) {

        if (activity[0] >= lastEnd) {
            count++;
            lastEnd = activity[1];
        }
    }

    return count;
}
```

### Why?

Earliest finishing activity leaves the most room for future activities.

### Complexity

``` text
O(n log n) time
O(1) auxiliary space excluding sort implementation/output
```

------------------------------------------------------------------------

# 64. Pattern Comparison

  Problem clue                       Pattern
  ---------------------------------- ----------------------
  kth largest                        min-heap size k
  kth smallest                       max-heap size k
  top k                              size-k heap
  repeatedly smallest                min-heap
  repeatedly largest                 max-heap
  merge intervals                    sort by start
  insert interval                    sorted interval scan
  maximum non-overlap                sort by end + greedy
  minimum removals for non-overlap   sort by end + greedy
  minimum rooms/resources            sort + min-heap
  next available resource            min-heap
  schedule by priority               heap + greedy

------------------------------------------------------------------------

# 65. Interview Explanations

## Explain Heap

> "A heap is a complete binary tree that satisfies a priority property.
> In a min-heap the smallest element is at the root, and in a max-heap
> the largest is at the root. Java's PriorityQueue provides heap
> functionality."

## Explain Kth Largest

> "Instead of sorting all elements, I maintain a min-heap of size k. The
> heap contains the k largest values seen so far, and its root is the
> smallest among them, which is the kth largest overall."

## Explain Merge Intervals

> "I sort intervals by start time, then scan once. If the next start is
> within the current end, I extend the current interval; otherwise I
> save the current interval and begin a new one."

## Explain Activity Selection

> "I sort by end time because choosing the earliest finishing compatible
> activity leaves the most room for future activities."

## Explain Meeting Rooms

> "I sort meetings by start time and maintain a min-heap of current
> meeting end times. The root is the earliest room to become available.
> If it is free before the next meeting starts, I reuse it; otherwise I
> need another room."

------------------------------------------------------------------------

# 66. Constraint Thinking

### n \<= 20

Exponential brute force may sometimes be possible.

### n \<= 10\^3

O(n²) may be acceptable depending on the language/time limit.

### n \<= 10\^5

Aim for:

``` text
O(n)
O(n log n)
```

For heap problems, ask:

``` text
Do I need all n values?
Or only top k?
```

If only k matters:

``` text
size-k heap
```

For interval problems:

``` text
Can sorting turn a complicated overlap problem into one scan?
```

------------------------------------------------------------------------

# 67. Common Interview Traps

### Trap 1

"Find kth largest" does **not** automatically mean max-heap.

Correct common pattern:

``` text
kth largest -> min-heap size k
```

### Trap 2

"Maximum number of non-overlapping intervals" does **not** mean sort by
start.

Correct greedy:

``` text
sort by end
```

### Trap 3

"Merge intervals" does **not** mean sort by end.

Use:

``` text
sort by start
```

### Trap 4

"Minimum meeting rooms" does not simply mean count total intervals.

You need maximum simultaneous overlap.

### Trap 5

A heap is not fully sorted.

### Trap 6

Greedy must have a valid justification.

------------------------------------------------------------------------

# 68. Practice Problems

## Easy

### 1. Kth Largest Element in a Stream

Pattern: min-heap.

https://leetcode.com/problems/kth-largest-element-in-a-stream/

### 2. Last Stone Weight

Pattern: max-heap.

https://leetcode.com/problems/last-stone-weight/

### 3. Merge Sorted Array

Pattern: sorted merging.

https://leetcode.com/problems/merge-sorted-array/

## Medium

### 4. Kth Largest Element in an Array

Pattern: size-k heap / quickselect.

https://leetcode.com/problems/kth-largest-element-in-an-array/

### 5. Top K Frequent Elements

Pattern: frequency + heap.

https://leetcode.com/problems/top-k-frequent-elements/

### 6. K Closest Points to Origin

Pattern: max-heap size k.

https://leetcode.com/problems/k-closest-points-to-origin/

### 7. Merge Intervals

Pattern: sort by start.

https://leetcode.com/problems/merge-intervals/

### 8. Insert Interval

Pattern: interval scan.

https://leetcode.com/problems/insert-interval/

### 9. Non-overlapping Intervals

Pattern: greedy + sort by end.

https://leetcode.com/problems/non-overlapping-intervals/

### 10. Meeting Rooms II

Pattern: intervals + min-heap.

https://leetcode.com/problems/meeting-rooms-ii/

### 11. Task Scheduler

Pattern: greedy + heap.

https://leetcode.com/problems/task-scheduler/

### 12. Find Median from Data Stream

Pattern: two heaps.

https://leetcode.com/problems/find-median-from-data-stream/

## Hard / Advanced

### 13. Merge k Sorted Lists

Pattern: min-heap.

https://leetcode.com/problems/merge-k-sorted-lists/

### 14. IPO

Pattern: greedy + heap.

https://leetcode.com/problems/ipo/

### 15. Minimum Number of Refueling Stops

Pattern: greedy + max-heap.

https://leetcode.com/problems/minimum-number-of-refueling-stops/

------------------------------------------------------------------------

# 69. Recommended Practice Order

### Round 1 --- Core

1.  Kth Largest Element in a Stream
2.  Last Stone Weight
3.  Kth Largest Element in an Array
4.  Merge Intervals
5.  Insert Interval

### Round 2 --- Placement Priority

6.  Top K Frequent Elements
7.  K Closest Points to Origin
8.  Non-overlapping Intervals
9.  Meeting Rooms II
10. Task Scheduler

### Round 3 --- Advanced

11. Find Median from Data Stream
12. Merge k Sorted Lists
13. IPO
14. Minimum Number of Refueling Stops

------------------------------------------------------------------------

# 70. Daily Test --- 10 Questions

## Q1

Java's default `PriorityQueue<Integer>` behaves as:

A. max-heap\
B. min-heap\
C. stack\
D. queue only

## Q2

For kth largest using a size-k heap, the common choice is:

A. max-heap\
B. min-heap\
C. deque\
D. stack

## Q3

`PriorityQueue.peek()` is typically:

A. O(n)\
B. O(log n)\
C. O(1)\
D. O(n log n)

## Q4

For merging intervals, sort primarily by:

A. start\
B. end\
C. length\
D. midpoint

## Q5

For maximum number of non-overlapping activities, sort by:

A. start descending\
B. end ascending\
C. length descending\
D. start ascending only

## Q6

Minimum meeting rooms commonly uses:

A. stack\
B. min-heap of end times\
C. binary search only\
D. HashSet

## Q7

A greedy algorithm:

A. always explores all combinations\
B. always uses recursion\
C. repeatedly makes a locally optimal choice\
D. always uses DP

## Q8

For kth smallest using a size-k heap, use:

A. min-heap\
B. max-heap\
C. deque\
D. queue

## Q9

Heap sort has typical time complexity:

A. O(n)\
B. O(log n)\
C. O(n log n)\
D. O(n²)

## Q10

For an interval problem, touching endpoints may or may not overlap
depending on:

A. Java version\
B. problem definition\
C. heap size\
D. array capacity

------------------------------------------------------------------------

# 71. Answer Key

``` text
Q1  -> B
Q2  -> B
Q3  -> C
Q4  -> A
Q5  -> B
Q6  -> B
Q7  -> C
Q8  -> B
Q9  -> C
Q10 -> B
```

Score guide:

``` text
9–10  Excellent
7–8   Good
5–6   Revise heap/interval patterns
0–4   Re-study the core sections
```

------------------------------------------------------------------------

# 72. Pattern Recognition Test

Identify the pattern.

### 1

"Return the kth largest value without sorting the entire array."

Answer:

``` text
min-heap of size k
```

### 2

"Continuously obtain the smallest available end time."

Answer:

``` text
min-heap
```

### 3

"Combine overlapping ranges."

Answer:

``` text
sort by start + merge
```

### 4

"Keep the maximum number of compatible activities."

Answer:

``` text
sort by end + greedy
```

### 5

"How many rooms are required for overlapping meetings?"

Answer:

``` text
sort by start + min-heap of end times
```

### 6

"Find the k closest points."

Answer:

``` text
max-heap of size k
```

### 7

"Find kth smallest."

Answer:

``` text
max-heap of size k
```

### 8

"Repeatedly select the best currently available job."

Answer:

``` text
greedy + priority queue
```

------------------------------------------------------------------------

# 73. Revision Drill

Before moving on, answer without looking:

``` text
1. What is the difference between min-heap and max-heap?
2. Why is kth largest commonly solved with a min-heap?
3. Why does a size-k heap save work compared with sorting?
4. What does PriorityQueue.peek() give?
5. What does PriorityQueue.poll() give?
6. What does heapify mean?
7. What is a greedy choice?
8. Why can greedy fail?
9. Why sort intervals by start for merging?
10. Why sort by end for activity selection?
11. Why does meeting-room scheduling need a heap?
12. What does the heap store in Meeting Rooms II?
13. What is the overlap condition?
14. Why does comparator subtraction sometimes cause overflow?
15. When should you suspect a top-k pattern?
```

------------------------------------------------------------------------

# 74. Java Templates

## Min Heap

``` java
PriorityQueue<Integer> minHeap = new PriorityQueue<>();
```

## Max Heap

``` java
PriorityQueue<Integer> maxHeap =
        new PriorityQueue<>(Collections.reverseOrder());
```

## Size-k Heap

``` java
for (int x : nums) {
    heap.offer(x);

    if (heap.size() > k) {
        heap.poll();
    }
}
```

## Sort Intervals by Start

``` java
Arrays.sort(
    intervals,
    (a, b) -> Integer.compare(a[0], b[0])
);
```

## Sort Intervals by End

``` java
Arrays.sort(
    intervals,
    (a, b) -> Integer.compare(a[1], b[1])
);
```

## Heap of End Times

``` java
PriorityQueue<Integer> endTimes = new PriorityQueue<>();

for (int[] interval : intervals) {

    if (!endTimes.isEmpty()
            && endTimes.peek() <= interval[0]) {
        endTimes.poll();
    }

    endTimes.offer(interval[1]);
}
```

------------------------------------------------------------------------

# 75. 30-Second Revision

``` text
HEAP
min -> smallest root
max -> largest root
peek -> O(1)
offer/poll -> O(log n)

TOP K
k largest -> min-heap size k
k smallest -> max-heap size k

GREEDY
local best choice
must justify correctness

INTERVALS
merge -> sort by start
maximum non-overlap -> sort by end
minimum rooms -> sort start + min-heap ends

JAVA
PriorityQueue = heap
Integer.compare = safe comparator
```

------------------------------------------------------------------------

# 76. Homework

## Mandatory

Complete:

1.  Kth Largest Element in an Array
2.  Top K Frequent Elements
3.  Merge Intervals
4.  Insert Interval
5.  Non-overlapping Intervals
6.  Meeting Rooms II
7.  Task Scheduler

## Recommended

8.  K Closest Points to Origin
9.  Find Median from Data Stream
10. Merge k Sorted Lists

## Challenge

11. IPO
12. Minimum Number of Refueling Stops

For every problem, write:

``` text
Pattern:
Brute force:
Bottleneck:
Optimization:
Time:
Space:
Edge cases:
```

------------------------------------------------------------------------

# 77. Day Completion Checklist

-   [ ] I understand min-heaps.
-   [ ] I understand max-heaps.
-   [ ] I can use Java PriorityQueue.
-   [ ] I know peek/offer/poll complexity.
-   [ ] I understand size-k heaps.
-   [ ] I can solve kth largest.
-   [ ] I can solve kth smallest.
-   [ ] I understand top-k frequency.
-   [ ] I understand heapify.
-   [ ] I know heap sort complexity.
-   [ ] I understand greedy algorithms.
-   [ ] I know why greedy can fail.
-   [ ] I understand activity selection.
-   [ ] I can merge intervals.
-   [ ] I can insert an interval.
-   [ ] I can remove minimum overlapping intervals.
-   [ ] I can check meeting conflicts.
-   [ ] I can solve minimum meeting rooms.
-   [ ] I recognize heap + interval combinations.
-   [ ] I know when to sort by start.
-   [ ] I know when to sort by end.
-   [ ] I completed the daily test.
-   [ ] I completed the mandatory problems.

------------------------------------------------------------------------

# 78. Final Interview Checklist

When you see:

``` text
kth largest
kth smallest
top k
```

ask:

``` text
Can a size-k heap avoid sorting everything?
```

When you see:

``` text
overlapping intervals
ranges
meetings
schedules
```

ask:

``` text
Should I sort by start?
Should I sort by end?
Do I need a heap for active intervals?
```

When you see:

``` text
maximum number of compatible activities
minimum removals for non-overlap
```

ask:

``` text
sort by end + greedy
```

When you see:

``` text
minimum rooms/resources
earliest available resource
```

ask:

``` text
sort by start + min-heap of end times
```

When you see:

``` text
repeatedly choose the best available option
```

ask:

``` text
greedy + PriorityQueue
```

------------------------------------------------------------------------

# 79. Final Mental Map

``` text
                    DAY 10
                       |
          +------------+------------+
          |            |            |
        HEAP         GREEDY      INTERVALS
          |            |            |
     +----+----+       |       +----+----+
     |         |       |       |    |    |
    MIN       MAX   local      start end overlap
     |         |    choice      |    |    |
   top-k    top-k   proof     merge  select rooms
     |                       insert greedy heap
 PriorityQueue
```

Core mental shortcuts:

``` text
k largest
→ min-heap size k

k smallest
→ max-heap size k

merge intervals
→ sort by start

maximum non-overlap
→ sort by end + greedy

minimum rooms
→ sort by start + min-heap of end times

repeated best available
→ PriorityQueue + greedy
```

------------------------------------------------------------------------

# 80. Day 10 Completion Standard

Do not move forward simply because you read this file.

Before Day 11, you should be able to code from memory:

``` text
1. Kth Largest
2. Top K Frequent
3. Merge Intervals
4. Insert Interval
5. Non-overlapping Intervals
6. Meeting Rooms II
```

And you should be able to explain:

``` text
why the chosen heap direction is correct;
why the interval sorting key is correct;
why the greedy choice is valid;
what the brute-force bottleneck is;
why the optimized solution is faster;
time complexity;
space complexity;
edge cases.
```

------------------------------------------------------------------------

# Navigation

**Previous:** [Day 9 --- Linked List + Stack +
Queue](Day-09-Linked-List-Stack-Queue.md)

**Next:** [Day 11 --- Trees](Day-11-Trees.md)
