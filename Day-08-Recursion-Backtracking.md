# 🔥 DAY 8 --- RECURSION + BACKTRACKING

## Today's Goal

Today you will learn:

> **Recursion**

> **Backtracking**

By the end of today you should be able to: - identify a base case and
recursive case - trace recursive calls and the call stack - write simple
recursive functions - understand recursion complexity - recognize
decision-tree problems - use the **Choose → Explore → Undo** pattern -
generate subsets, permutations, combinations, and combinations summing
to a target - solve valid-parentheses and grid-search style problems -
understand N-Queens at interview level - prune impossible branches -
avoid state-restoration bugs

# 1. PREREQUISITES

You already know Java methods, arrays, strings, loops, complexity, two
pointers, sliding window, sorting, and binary search.

Today does not repeat those topics. The focus is a new problem-solving
model:

``` text
Problem
   ↓
Smaller version of the same problem
   ↓
Solve recursively
   ↓
Build the answer
```

# 2. PRIORITY

  Topic                   Priority
  ----------------------- ------------
  Recursion basics        🔥🔥🔥🔥🔥
  Base case               🔥🔥🔥🔥🔥
  Call stack              🔥🔥🔥🔥
  Recursion tracing       🔥🔥🔥🔥🔥
  Subsets                 🔥🔥🔥🔥🔥
  Permutations            🔥🔥🔥🔥🔥
  Combinations            🔥🔥🔥🔥
  Combination Sum         🔥🔥🔥🔥🔥
  Backtracking template   🔥🔥🔥🔥🔥
  Generate Parentheses    🔥🔥🔥🔥
  Grid Backtracking       🔥🔥🔥🔥
  N-Queens                🔥🔥🔥🔥
  Pruning                 🔥🔥🔥🔥
  Pattern Recognition     🔥🔥🔥🔥🔥

# 3. WHAT IS RECURSION?

## 🧑‍🎓 Beginner Explanation

Recursion means:

> **A function calls itself to solve a smaller version of the same
> problem.**

A recursive solution normally has two parts:

``` text
1. Base Case
2. Recursive Case
```

The base case stops recursion. The recursive case makes progress toward
that base case.

Bad:

``` java
void solve(int n) {
    solve(n - 1);
}
```

There is no stopping condition.

Good:

``` java
void solve(int n) {
    if (n == 0) {
        return;
    }

    solve(n - 1);
}
```

### 30-Second Revision

``` text
Recursion = function calls itself
Base case = stop
Recursive case = smaller problem
```

# 4. COUNTDOWN --- FIRST RECURSION EXAMPLE

### Problem

Print:

``` text
5
4
3
2
1
```

### Approach

Base case:

``` text
n == 0
```

Recursive step:

``` text
solve(n - 1)
```

### Java

``` java
public static void countdown(int n) {

    if (n == 0) {
        return;
    }

    System.out.println(n);

    countdown(n - 1);
}
```

### Dry Run

``` text
countdown(5)
 → print 5
 → countdown(4)
    → print 4
    → countdown(3)
       → print 3
       → countdown(2)
          → print 2
          → countdown(1)
             → print 1
             → countdown(0)
                → return
```

### Complexity

``` text
Time:  O(n)
Space: O(n)   // recursion stack
```

# 5. CALL STACK

Every active function call occupies a stack frame.

For:

``` java
countdown(3);
```

the stack grows approximately like:

``` text
countdown(3)
countdown(2)
countdown(1)
countdown(0)
```

Then it unwinds:

``` text
countdown(0) returns
countdown(1) returns
countdown(2) returns
countdown(3) returns
```

Think:

``` text
GOING DOWN  → recursive calls
COMING UP   → return phase
```

Statements before the recursive call execute while going down.

Statements after the recursive call execute while coming back up.

Example:

``` java
public static void demo(int n) {

    if (n == 0) {
        return;
    }

    System.out.println("Before " + n);

    demo(n - 1);

    System.out.println("After " + n);
}
```

For `demo(3)`:

``` text
Before 3
Before 2
Before 1
After 1
After 2
After 3
```

# 6. BASE CASE + RECURSIVE PROGRESS

A base case must be reachable.

If:

``` text
n decreases
```

then a natural base may be:

``` java
if (n == 0) return;
```

The recursive call must move toward it.

``` java
solve(n - 1);  // progress toward 0
```

is appropriate.

``` java
solve(n + 1);  // moves away from 0
```

can cause infinite recursion and eventually:

``` text
StackOverflowError
```

### Base-case checklist

``` text
☐ Can the base case actually be reached?
☐ Does it stop recursion?
☐ Is it correct for the smallest input?
☐ Does every recursive call make progress?
```

# 7. FACTORIAL

Factorial has a natural recursive definition:

``` text
n! = n × (n-1)!
0! = 1
```

### Java

``` java
public static long factorial(int n) {

    if (n == 0) {
        return 1;
    }

    return n * factorial(n - 1);
}
```

### Dry Run

``` text
factorial(5)
= 5 * factorial(4)
= 5 * 4 * factorial(3)
= 5 * 4 * 3 * factorial(2)
= 5 * 4 * 3 * 2 * factorial(1)
= 5 * 4 * 3 * 2 * 1 * factorial(0)
= 120
```

### Complexity

``` text
Time:  O(n)
Space: O(n)
```

# 8. SUM OF FIRST N NUMBERS

``` java
public static int sum(int n) {

    if (n == 0) {
        return 0;
    }

    return n + sum(n - 1);
}
```

For:

``` text
sum(5)
```

``` text
5 + 4 + 3 + 2 + 1 = 15
```

Complexity:

``` text
Time:  O(n)
Space: O(n)
```

# 9. RECURSIVE ARRAY TRAVERSAL

Instead of a loop, use the index as state.

``` java
public static void printArray(int[] arr, int index) {

    if (index == arr.length) {
        return;
    }

    System.out.println(arr[index]);

    printArray(arr, index + 1);
}
```

State:

``` text
index
```

Base:

``` text
index == arr.length
```

Progress:

``` text
index + 1
```

This same state/index idea appears constantly in backtracking.

# 10. RECURSION TEMPLATE

``` java
returnType solve(parameters) {

    if (baseCondition) {
        return baseAnswer;
    }

    return solve(smallerProblem);
}
```

For `void`:

``` java
void solve(parameters) {

    if (baseCondition) {
        return;
    }

    solve(smallerProblem);
}
```

### Pattern

``` text
Base
 ↓
Make problem smaller
 ↓
Recursive call
```

# 11. RECURSION VS ITERATION

  Recursion                        Iteration
  -------------------------------- --------------------------------
  Function calls itself            Loop repeats
  Uses call stack                  Usually O(1) extra stack
  Natural for trees/backtracking   Often simpler for linear tasks
  Can be elegant                   Often more memory-efficient
  Can overflow stack               No recursion-stack overflow

Recursion is not automatically better. Use it when the problem structure
naturally fits it.

# 12. FIBONACCI --- WHY RECURSION CAN BE EXPENSIVE

Naive Fibonacci:

``` java
public static int fib(int n) {

    if (n <= 1) {
        return n;
    }

    return fib(n - 1) + fib(n - 2);
}
```

The problem is repeated work.

``` text
fib(5)
├── fib(4)
│   ├── fib(3)
│   └── fib(2)
└── fib(3)
    ├── fib(2)
    └── fib(1)
```

The same subproblems are recalculated.

The naive recursive version has exponential growth, commonly described
as approximately:

``` text
O(2^n)
```

This is an important bridge to Dynamic Programming later.

### Lesson

> Elegant recursion does not automatically mean efficient recursion.

# 13. WHEN SHOULD YOU THINK RECURSION?

Look for phrases such as:

``` text
smaller version of the same problem
tree traversal
divide and conquer
generate all
choose
explore
partition
subsets
permutations
combinations
paths
```

For "generate all possibilities", recursion often becomes backtracking.

# 14. WHAT IS BACKTRACKING?

## 🧑‍🎓 Beginner Explanation

Backtracking is:

> **Recursion + choices + undoing the choice.**

The most important mental model:

``` text
CHOOSE
  ↓
EXPLORE
  ↓
UNDO
```

At every step:

``` text
What choices are available?
```

Pick one.

Explore that branch.

Undo it.

Try the next choice.

# 15. DECISION TREE

Suppose we need all subsets of:

``` text
[1,2]
```

For every element:

``` text
take it
or
skip it
```

Decision tree:

``` text
                 []
              /                 take 1   skip 1
             /                    [1]          []
          /   \        /          +2     -2     +2    -2
       |       |      |      |
    [1,2]     [1]    [2]    []
```

Backtracking explores this tree without writing separate code for every
branch.

# 16. GENERIC BACKTRACKING TEMPLATE

``` java
void backtrack(state) {

    if (isComplete(state)) {
        result.add(copy(state));
        return;
    }

    for (Choice choice : choices) {

        if (!isValid(choice, state)) {
            continue;
        }

        makeChoice(choice, state);

        backtrack(nextState);

        undoChoice(choice, state);
    }
}
```

Memorize:

``` text
1. Check complete
2. Loop through choices
3. Reject invalid choices
4. Make choice
5. Recurse
6. Undo
```

# 17. WHY DO WE UNDO?

Suppose:

``` text
path = [1]
```

Choose `2`:

``` text
path = [1,2]
```

After exploring that branch, the next branch must start from:

``` text
[1]
```

not:

``` text
[1,2]
```

Therefore:

``` java
path.add(choice);

backtrack(...);

path.remove(path.size() - 1);
```

The final line restores the state.

### Golden Rule

> **Undo exactly what you changed.**

# 18. SUBSETS

For:

``` text
[1,2,3]
```

subsets include:

``` text
[]
[1]
[2]
[3]
[1,2]
[1,3]
[2,3]
[1,2,3]
```

Every element has two choices:

``` text
include
exclude
```

Therefore:

``` text
number of subsets = 2^n
```

# 19. SUBSETS JAVA

``` java
import java.util.*;

public static List<List<Integer>> subsets(int[] nums) {

    List<List<Integer>> result = new ArrayList<>();

    backtrack(nums, 0, new ArrayList<>(), result);

    return result;
}

private static void backtrack(
        int[] nums,
        int start,
        List<Integer> path,
        List<List<Integer>> result) {

    result.add(new ArrayList<>(path));

    for (int i = start; i < nums.length; i++) {

        path.add(nums[i]);

        backtrack(nums, i + 1, path, result);

        path.remove(path.size() - 1);
    }
}
```

### Why `i + 1`?

Once we choose index `i`, we move forward so the same position is not
selected again.

### Why copy `path`?

Because `path` is mutable:

``` java
result.add(new ArrayList<>(path));
```

If you store the same object repeatedly, later modifications affect
previously stored results.

# 20. SUBSETS DRY RUN

Input:

``` text
[1,2]
```

Start:

``` text
path = []
```

Record:

``` text
[]
```

Choose `1`:

``` text
[1]
```

Record.

Choose `2`:

``` text
[1,2]
```

Record.

Undo `2`:

``` text
[1]
```

Undo `1`:

``` text
[]
```

Choose `2`:

``` text
[2]
```

Record.

Undo:

``` text
[]
```

Result:

``` text
[]
[1]
[1,2]
[2]
```

Order is normally irrelevant unless the problem specifies one.

# 21. SUBSETS COMPLEXITY

There are:

``` text
2^n
```

subsets.

Copying each subset can take up to `O(n)`.

Therefore output-sensitive time:

``` text
O(n × 2^n)
```

Auxiliary recursion/path space:

``` text
O(n)
```

Output space:

``` text
O(n × 2^n)
```

# 22. PERMUTATIONS

Permutations ask:

> Which unused element should come next?

For:

``` text
[1,2,3]
```

we get:

``` text
[1,2,3]
[1,3,2]
[2,1,3]
[2,3,1]
[3,1,2]
[3,2,1]
```

Number of permutations:

``` text
n!
```

Unlike subsets, order matters.

# 23. PERMUTATIONS JAVA

``` java
public static List<List<Integer>> permute(int[] nums) {

    List<List<Integer>> result = new ArrayList<>();

    boolean[] used = new boolean[nums.length];

    backtrack(nums, used, new ArrayList<>(), result);

    return result;
}

private static void backtrack(
        int[] nums,
        boolean[] used,
        List<Integer> path,
        List<List<Integer>> result) {

    if (path.size() == nums.length) {
        result.add(new ArrayList<>(path));
        return;
    }

    for (int i = 0; i < nums.length; i++) {

        if (used[i]) {
            continue;
        }

        used[i] = true;
        path.add(nums[i]);

        backtrack(nums, used, path, result);

        path.remove(path.size() - 1);
        used[i] = false;
    }
}
```

The order is:

``` text
mark used
add
recurse
remove
unmark
```

# 24. PERMUTATION COMPLEXITY

There are:

``` text
n!
```

permutations.

Copying an answer costs up to `O(n)`.

Therefore:

``` text
Time: O(n × n!)
Auxiliary Space: O(n)
Output Space: O(n × n!)
```

# 25. COMBINATIONS

Combination means choosing a fixed number of elements where order does
not matter.

Example:

``` text
n = 4
k = 2
```

Results:

``` text
[1,2]
[1,3]
[1,4]
[2,3]
[2,4]
[3,4]
```

We do not separately generate:

``` text
[2,1]
```

because it represents the same combination as `[1,2]`.

Use a `start` index to maintain forward progress.

# 26. COMBINATIONS JAVA

``` java
public static List<List<Integer>> combine(int n, int k) {

    List<List<Integer>> result = new ArrayList<>();

    backtrack(1, n, k, new ArrayList<>(), result);

    return result;
}

private static void backtrack(
        int start,
        int n,
        int k,
        List<Integer> path,
        List<List<Integer>> result) {

    if (path.size() == k) {
        result.add(new ArrayList<>(path));
        return;
    }

    for (int i = start; i <= n; i++) {

        path.add(i);

        backtrack(i + 1, n, k, path, result);

        path.remove(path.size() - 1);
    }
}
```

The key:

``` java
backtrack(i + 1, ...)
```

means we cannot reuse the current position and do not generate reordered
duplicates.

# 27. SUBSETS VS COMBINATIONS VS PERMUTATIONS

  Pattern           Order Matters?   Reuse?         Main State
  ----------------- ---------------- -------------- -----------------------
  Subsets           No               No             start + path
  Combinations      No               No             start + path
  Permutations      Yes              No             used + path
  Combination Sum   No               Yes, usually   start + target + path

Remember:

``` text
Subsets → include/skip
Combinations → move start forward
Permutations → choose unused
```

# 28. COMBINATION SUM

Example:

``` text
candidates = [2,3,6,7]
target = 7
```

Valid answers:

``` text
[2,2,3]
[7]
```

The same candidate may be reused.

Therefore after choosing index `i`, recurse with:

``` java
i
```

not:

``` java
i + 1
```

This is a major interview distinction.

# 29. COMBINATION SUM JAVA

``` java
public static List<List<Integer>> combinationSum(
        int[] candidates,
        int target) {

    List<List<Integer>> result = new ArrayList<>();

    Arrays.sort(candidates);

    backtrack(
        candidates,
        target,
        0,
        new ArrayList<>(),
        result
    );

    return result;
}

private static void backtrack(
        int[] candidates,
        int target,
        int start,
        List<Integer> path,
        List<List<Integer>> result) {

    if (target == 0) {
        result.add(new ArrayList<>(path));
        return;
    }

    for (int i = start; i < candidates.length; i++) {

        if (candidates[i] > target) {
            break;
        }

        path.add(candidates[i]);

        backtrack(
            candidates,
            target - candidates[i],
            i,
            path,
            result
        );

        path.remove(path.size() - 1);
    }
}
```

Sorting is not required for the basic concept, but it enables useful
pruning:

``` java
if (candidates[i] > target) break;
```

because later candidates are also too large.

# 30. PRUNING

Pruning means:

> **Stop exploring a branch as soon as you know it cannot produce a
> valid answer.**

Example:

``` text
target = 7
current selected sum = 10
```

If all values are positive, this branch cannot become valid.

So stop.

Common pruning:

``` java
if (target < 0) return;
```

or:

``` java
if (!isValid(choice)) continue;
```

Pruning does not change the worst-case exponential nature of many
backtracking problems, but it can dramatically reduce the actual search.

# 31. GENERATE PARENTHESES

Given:

``` text
n = 3
```

generate:

``` text
((()))
(()())
(())()
()(())
()()()
```

At every step we may add:

``` text
(
```

or:

``` text
)
```

but only when valid.

Rules:

``` text
open < n
```

allows another opening parenthesis.

``` text
close < open
```

allows a closing parenthesis.

This prevents a prefix from ever having more closing parentheses than
opening parentheses.

# 32. GENERATE PARENTHESES JAVA

``` java
public static List<String> generateParenthesis(int n) {

    List<String> result = new ArrayList<>();

    backtrack(
        n,
        0,
        0,
        new StringBuilder(),
        result
    );

    return result;
}

private static void backtrack(
        int n,
        int open,
        int close,
        StringBuilder path,
        List<String> result) {

    if (path.length() == 2 * n) {
        result.add(path.toString());
        return;
    }

    if (open < n) {

        path.append('(');

        backtrack(
            n,
            open + 1,
            close,
            path,
            result
        );

        path.deleteCharAt(path.length() - 1);
    }

    if (close < open) {

        path.append(')');

        backtrack(
            n,
            open,
            close + 1,
            path,
            result
        );

        path.deleteCharAt(path.length() - 1);
    }
}
```

### Java-specific lesson

Use `StringBuilder` for mutable path state:

``` text
append → recurse → delete
```

rather than repeatedly creating new strings.

# 33. GRID BACKTRACKING

Backtracking can explore a 2D grid.

Typical choices:

``` text
up
down
left
right
```

Typical state:

``` text
row
column
index in target
visited state
```

Typical cycle:

``` text
match current cell
↓
mark visited
↓
explore neighbors
↓
restore cell
```

# 34. WORD SEARCH

For a word-search problem:

``` text
A B C E
S F C S
A D E E
```

and:

``` text
ABCCED
```

we start from every possible matching cell.

At each cell:

``` text
if character does not match → return false
if word is complete → return true
mark current cell
explore 4 neighbors
restore current cell
```

This is recursion + state restoration.

# 35. WORD SEARCH JAVA

``` java
public static boolean exist(
        char[][] board,
        String word) {

    for (int r = 0; r < board.length; r++) {

        for (int c = 0; c < board[0].length; c++) {

            if (dfs(board, word, r, c, 0)) {
                return true;
            }
        }
    }

    return false;
}

private static boolean dfs(
        char[][] board,
        String word,
        int row,
        int col,
        int index) {

    if (index == word.length()) {
        return true;
    }

    if (row < 0 ||
        row >= board.length ||
        col < 0 ||
        col >= board[0].length) {
        return false;
    }

    if (board[row][col] != word.charAt(index)) {
        return false;
    }

    char original = board[row][col];

    board[row][col] = '#';

    boolean found =
        dfs(board, word, row + 1, col, index + 1)
        || dfs(board, word, row - 1, col, index + 1)
        || dfs(board, word, row, col + 1, index + 1)
        || dfs(board, word, row, col - 1, index + 1);

    board[row][col] = original;

    return found;
}
```

The crucial line is:

``` java
board[row][col] = original;
```

Without restoration, a failed branch can incorrectly affect another
branch.

# 36. N-QUEENS

N-Queens asks us to place `n` queens on an `n × n` board so that no two
queens attack each other.

A useful strategy:

> Place exactly one queen in each row.

For each row:

``` text
try every column
↓
reject unsafe positions
↓
place queen
↓
recurse to next row
↓
remove queen
```

A queen conflicts when it shares:

``` text
column
main diagonal
anti-diagonal
```

For positions `(r1,c1)` and `(r2,c2)`:

``` text
same column:
c1 == c2

same main diagonal:
r1 - c1 == r2 - c2

same anti-diagonal:
r1 + c1 == r2 + c2
```

# 37. N-QUEENS JAVA

``` java
public static List<List<String>> solveNQueens(int n) {

    List<List<String>> result = new ArrayList<>();

    char[][] board = new char[n][n];

    for (int r = 0; r < n; r++) {
        Arrays.fill(board[r], '.');
    }

    boolean[] columns = new boolean[n];
    boolean[] diag1 = new boolean[2 * n - 1];
    boolean[] diag2 = new boolean[2 * n - 1];

    backtrack(
        0,
        n,
        board,
        columns,
        diag1,
        diag2,
        result
    );

    return result;
}

private static void backtrack(
        int row,
        int n,
        char[][] board,
        boolean[] columns,
        boolean[] diag1,
        boolean[] diag2,
        List<List<String>> result) {

    if (row == n) {

        List<String> solution = new ArrayList<>();

        for (char[] r : board) {
            solution.add(new String(r));
        }

        result.add(solution);
        return;
    }

    for (int col = 0; col < n; col++) {

        int d1 = row - col + n - 1;
        int d2 = row + col;

        if (columns[col] || diag1[d1] || diag2[d2]) {
            continue;
        }

        board[row][col] = 'Q';
        columns[col] = true;
        diag1[d1] = true;
        diag2[d2] = true;

        backtrack(
            row + 1,
            n,
            board,
            columns,
            diag1,
            diag2,
            result
        );

        board[row][col] = '.';
        columns[col] = false;
        diag1[d1] = false;
        diag2[d2] = false;
    }
}
```

The arrays make validity checking approximately `O(1)` per attempted
placement.

# 38. N-QUEENS COMPLEXITY

The search space is exponential.

A common interview-level upper-bound description is:

``` text
O(n!)
```

for the backtracking search, ignoring output representation details.

Space includes:

``` text
Board: O(n²)
Tracking arrays: O(n)
Recursion: O(n)
```

Therefore the board itself dominates auxiliary state at:

``` text
O(n²)
```

excluding the returned solutions.

# 39. BACKTRACKING STATE DESIGN

Every backtracking problem can be decomposed into state.

  Problem           State
  ----------------- ----------------------------------------
  Subsets           start/index + path
  Permutations      used + path
  Combinations      start + path
  Combination Sum   start + target + path
  Parentheses       open + close + path
  Word Search       row + col + word index + visited state
  N-Queens          row + columns + diagonals + board

This is one of the most useful interview habits:

> Before coding, write down the minimum state needed to describe one
> recursive position.

# 40. REUSE VS NO REUSE

This is a frequent source of bugs.

### No reuse

After choosing index `i`:

``` java
backtrack(i + 1);
```

### Reuse allowed

Stay at `i`:

``` java
backtrack(i);
```

Example:

``` text
Combination Sum → reuse allowed
```

Therefore:

``` java
backtrack(i);
```

For a combination where every input element can be used once:

``` java
backtrack(i + 1);
```

# 41. SUBSETS VS PERMUTATIONS

### Subsets

Order does not matter.

``` text
[1,2]
```

and:

``` text
[2,1]
```

represent the same selected set.

Use forward index progression.

### Permutations

Order matters.

``` text
[1,2]
```

and:

``` text
[2,1]
```

are different.

Use all unused elements at every position.

### Quick memory trick

``` text
Subsets → choose or skip
Permutations → choose unused
```

# 42. DUPLICATES IN BACKTRACKING

For duplicate input values, sorting can help.

Example:

``` text
[1,2,2]
```

At the same recursion level, selecting the first `2` and the second `2`
can create duplicate answers.

A common pattern for unique combinations is:

``` java
Arrays.sort(nums);

if (i > start && nums[i] == nums[i - 1]) {
    continue;
}
```

Important:

> This usually skips duplicate choices at the same recursion depth. Do
> not blindly skip every repeated value at every depth.

# 43. BRUTE FORCE → BACKTRACKING

Suppose we need all valid arrangements.

Naive approach:

``` text
Generate everything
↓
Check every complete arrangement
```

Backtracking:

``` text
Make a choice
↓
Check validity immediately
↓
If invalid, stop
↓
Otherwise recurse
↓
Undo
```

The improvement is primarily from **pruning the search tree early**.

Backtracking can still be exponential. It is not a magic way to make
exponential problems polynomial.

# 44. COMPLEXITY THINKING FOR RECURSION

Ask three questions:

``` text
1. How many branches does each call create?
2. How deep can recursion go?
3. How much work happens at each node?
```

Examples:

### One branch per level

Often:

``` text
O(n)
```

### Two choices per level

Potentially:

``` text
O(2^n)
```

### All permutations

Potentially:

``` text
O(n!)
```

Always account for output construction when a problem asks you to return
many objects.

# 45. COMMON BEGINNER MISTAKES

## Mistake 1 --- No base case

Leads to infinite recursion.

## Mistake 2 --- Base case is unreachable

The recursive state never reaches the stopping condition.

## Mistake 3 --- Forgetting to undo

``` java
path.add(x);
backtrack(...);
// missing remove
```

Branches contaminate each other.

## Mistake 4 --- Storing the same mutable path

Use:

``` java
new ArrayList<>(path)
```

when storing a list result.

## Mistake 5 --- Wrong index progression

``` text
i + 1 → no reuse
i     → reuse
```

## Mistake 6 --- Forgetting to unmark used

``` java
used[i] = true;
...
used[i] = false;
```

## Mistake 7 --- No pruning

If a branch is already impossible, stop it immediately.

## Mistake 8 --- Confusing combinations and permutations

Ask:

> Does order matter?

# 46. EDGE CASES

Test:

``` text
empty input
one element
n = 0 where allowed
target = 0
target smaller than all candidates
no valid solution
exactly one solution
many solutions
duplicate values
all values equal
already-invalid state
```

For recursion, always test the smallest valid input because it usually
triggers the base case.

# 47. JAVA-SPECIFIC DSA NOTES

### Mutable list

``` java
path.add(x);
path.remove(path.size() - 1);
```

### Copy before storing

``` java
result.add(new ArrayList<>(path));
```

### Mutable string path

``` java
StringBuilder path
```

Use:

``` java
path.append('x');
path.deleteCharAt(path.length() - 1);
```

### Boolean tracking

``` java
boolean[] used
```

Always restore:

``` java
used[i] = false;
```

### Grid restoration

``` java
char original = board[r][c];
board[r][c] = '#';

dfs(...);

board[r][c] = original;
```

# 48. INTERVIEW EXPLANATION --- RECURSION

A strong answer:

> "I define the problem in terms of a smaller instance of itself. I
> identify a base case that can be answered directly, then recursively
> solve the smaller state. Every recursive call moves toward the base
> case, which guarantees termination for valid inputs."

# 49. INTERVIEW EXPLANATION --- BACKTRACKING

A strong answer:

> "This problem requires exploring multiple possible choices. I maintain
> the current state, choose one candidate, recursively explore that
> branch, and then undo the choice before trying the next candidate. I
> prune choices as soon as I know they cannot lead to a valid solution."

# 50. INTERVIEW EXPLANATION --- SUBSETS

A strong answer:

> "For every element I have two choices: include it or skip it. This
> creates `2^n` possible subsets. I use a recursive path to represent
> the current subset and copy that path into the result at each valid
> state."

# 51. INTERVIEW EXPLANATION --- PERMUTATIONS

A strong answer:

> "At every position I can select any element that has not been used. I
> track selected elements with a boolean array, add a choice, recurse,
> then remove the choice and mark it unused again. There are `n!`
> permutations for `n` distinct elements."

# 52. INTERVIEW EXPLANATION --- N-QUEENS

A strong answer:

> "I place one queen per row. For each row I try every column, reject
> columns or diagonals that are already occupied, recurse to the next
> row, and then undo the placement. Column and diagonal boolean arrays
> let me check validity in constant time."

# 53. CONSTRAINT THINKING

Backtracking is appropriate when the search space is small enough or
when constraints allow strong pruning.

Examples:

``` text
Subsets → 2^n
Permutations → n!
```

Therefore:

``` text
n = 10
```

can be manageable for subsets:

``` text
2^10 = 1024
```

but:

``` text
n = 50
```

gives:

``` text
2^50
```

which is enormous.

Always inspect constraints before choosing brute force/backtracking.

# 54. MINI PRACTICE --- BINARY STRINGS

## Problem

Generate all binary strings of length `n`.

For:

``` text
n = 3
```

expected strings:

``` text
000
001
010
011
100
101
110
111
```

### Hint

At each position:

``` text
choice 1 → 0
choice 2 → 1
```

State:

``` text
position + path
```

Base:

``` text
position == n
```

Complexity:

``` text
O(n × 2^n)
```

including copying each generated string.

# 55. MINI PRACTICE --- CHOOSE K

## Problem

Generate all ways to choose `k = 2` numbers from `1..4`.

Expected:

``` text
[1,2]
[1,3]
[1,4]
[2,3]
[2,4]
[3,4]
```

### Hint

Use:

``` text
start
path
```

After choosing `i`:

``` java
backtrack(i + 1);
```

because each number can be used once and order does not matter.

# 56. FULL PRACTICE --- SUBSETS

### Input

``` text
nums = [1,2,3]
```

### Observation

Each value can be selected or skipped.

### Pattern

``` text
Backtracking
```

### Code

``` java
public static List<List<Integer>> subsets(int[] nums) {

    List<List<Integer>> result = new ArrayList<>();

    backtrack(nums, 0, new ArrayList<>(), result);

    return result;
}

private static void backtrack(
        int[] nums,
        int start,
        List<Integer> path,
        List<List<Integer>> result) {

    result.add(new ArrayList<>(path));

    for (int i = start; i < nums.length; i++) {

        path.add(nums[i]);

        backtrack(nums, i + 1, path, result);

        path.remove(path.size() - 1);
    }
}
```

### Dry Run

``` text
[]
 ├── choose 1 → [1]
 │      ├── choose 2 → [1,2]
 │      └── choose 3 → [1,3]
 ├── choose 2 → [2]
 │      └── choose 3 → [2,3]
 └── choose 3 → [3]
```

### Complexity

``` text
Time: O(n × 2^n)
Auxiliary: O(n)
Output: O(n × 2^n)
```

# 57. FULL PRACTICE --- PERMUTATIONS

### Input

``` text
[1,2,3]
```

### Observation

Order matters, so every position can choose any currently unused
element.

### Code

``` java
public static List<List<Integer>> permute(int[] nums) {

    List<List<Integer>> result = new ArrayList<>();
    boolean[] used = new boolean[nums.length];

    backtrack(nums, used, new ArrayList<>(), result);

    return result;
}

private static void backtrack(
        int[] nums,
        boolean[] used,
        List<Integer> path,
        List<List<Integer>> result) {

    if (path.size() == nums.length) {
        result.add(new ArrayList<>(path));
        return;
    }

    for (int i = 0; i < nums.length; i++) {

        if (used[i]) {
            continue;
        }

        used[i] = true;
        path.add(nums[i]);

        backtrack(nums, used, path, result);

        path.remove(path.size() - 1);
        used[i] = false;
    }
}
```

### Complexity

``` text
Time: O(n × n!)
Auxiliary: O(n)
Output: O(n × n!)
```

# 58. FULL PRACTICE --- COMBINATION SUM

### Input

``` text
candidates = [2,3,6,7]
target = 7
```

### Output

``` text
[2,2,3]
[7]
```

### Key observation

Reuse is allowed.

Therefore:

``` java
backtrack(..., i, ...)
```

not:

``` java
backtrack(..., i + 1, ...)
```

### Important pruning

After sorting:

``` java
if (candidates[i] > target) {
    break;
}
```

### Complexity

The worst-case search is exponential; exact bounds depend on candidate
values and target. The important interview point is that the
output/search tree can grow exponentially.

# 59. FULL PRACTICE --- GENERATE PARENTHESES

### Input

``` text
n = 3
```

### State

``` text
open
close
path
```

### Rules

``` text
open < n
close < open
```

### Base case

``` text
path.length() == 2*n
```

### Code

``` java
public static List<String> generateParenthesis(int n) {

    List<String> result = new ArrayList<>();

    backtrack(n, 0, 0, new StringBuilder(), result);

    return result;
}

private static void backtrack(
        int n,
        int open,
        int close,
        StringBuilder path,
        List<String> result) {

    if (path.length() == 2 * n) {
        result.add(path.toString());
        return;
    }

    if (open < n) {
        path.append('(');
        backtrack(n, open + 1, close, path, result);
        path.deleteCharAt(path.length() - 1);
    }

    if (close < open) {
        path.append(')');
        backtrack(n, open, close + 1, path, result);
        path.deleteCharAt(path.length() - 1);
    }
}
```

# 60. FULL PRACTICE --- WORD SEARCH

### Pattern

``` text
Grid
+
DFS
+
Visited state
+
Undo
```

### Algorithm

``` text
For every cell:
    if it can start the word:
        mark it
        explore 4 neighbors
        restore it
```

### Complexity

A standard upper-bound discussion is exponential in the word length,
with at most `O(m*n*4^L)` style search before considering pruning, where
`L` is word length. The exact practical work is reduced by character
checks and the visited constraint.

### Important interview point

The restoration step:

``` java
board[row][col] = original;
```

is what allows a different search branch to reuse that cell later.

# 61. PATTERN COMPARISON

  Clue                                  Pattern
  ------------------------------------- ------------------------
  Smaller version of same problem       Recursion
  Generate all subsets                  Backtracking
  Generate all permutations             Backtracking + used
  Generate fixed-size combinations      Backtracking + start
  Candidate can be reused               Recurse with `i`
  Candidate cannot be reused            Recurse with `i + 1`
  Generate valid arrangements           Backtracking + pruning
  Grid path without reuse               DFS + Backtracking
  Place objects under constraints       Backtracking
  Many repeated recursive subproblems   Consider DP later

# 62. QUICK DECISION TREE

``` text
Does the problem ask for all possibilities?
        |
       YES
        ↓
Can I describe choices at each step?
        |
       YES
        ↓
Backtracking

What does one level represent?
        |
        ├── Element position → subsets/permutations
        ├── Start index → combinations
        ├── Target remaining → combination sum
        ├── Open/close count → parentheses
        ├── Grid cell → grid DFS
        └── Board row → N-Queens
```

# 63. MUST-MEMORIZE TEMPLATES

### Basic recursion

``` java
void solve(int state) {

    if (baseCondition) {
        return;
    }

    solve(smallerState);
}
```

### Generic backtracking

``` java
void backtrack(State state) {

    if (complete(state)) {
        result.add(copy(state));
        return;
    }

    for (Choice choice : choices) {

        if (!valid(choice, state)) {
            continue;
        }

        makeChoice(choice, state);

        backtrack(nextState);

        undoChoice(choice, state);
    }
}
```

### Path

``` java
path.add(choice);
backtrack(...);
path.remove(path.size() - 1);
```

### Used

``` java
used[i] = true;
path.add(nums[i]);

backtrack(...);

path.remove(path.size() - 1);
used[i] = false;
```

# 64. DAILY TEST --- 10 QUESTIONS

## Q1

A recursive solution normally needs:

A. HashMap + Set\
B. Base case + recursive case\
C. Stack + Queue\
D. Sort + Search

## Q2

The purpose of a base case is:

A. Sort data\
B. Stop recursion\
C. Increase branching\
D. Create an array

## Q3

Backtracking follows:

A. Sort → Search → Merge\
B. Choose → Explore → Undo\
C. Push → Pop → Peek\
D. Divide → Multiply → Add

## Q4

Number of subsets of `n` unique elements:

A. `n`\
B. `n²`\
C. `2^n`\
D. `n!`

## Q5

Number of permutations of `n` distinct elements:

A. `2^n`\
B. `n`\
C. `n²`\
D. `n!`

## Q6

What tracks whether an element is already selected in permutation
backtracking?

A. `used[]`\
B. Prefix sum\
C. Queue\
D. Binary search

## Q7

If reuse is allowed in Combination Sum, after choosing index `i` we
generally recurse with:

A. `i + 1`\
B. `i`\
C. `n - 1`\
D. `0` always

## Q8

Why copy `path` before storing it?

A. To sort it\
B. Because `path` is mutable\
C. To reduce recursion\
D. To remove all duplicates

## Q9

Pruning means:

A. Sorting the output\
B. Stopping an impossible branch early\
C. Adding another recursive branch\
D. Increasing the search space

## Q10

A standard N-Queens strategy is:

A. Place one queen per row\
B. Put all queens in one row\
C. Use sliding window\
D. Use binary search

# 65. ANSWER KEY

``` text
Q1 → B
Q2 → B
Q3 → B
Q4 → C
Q5 → D
Q6 → A
Q7 → B
Q8 → B
Q9 → B
Q10 → A
```

# 66. PATTERN RECOGNITION TEST

## Problem A

Generate every subset of an array.

``` text
Pattern:
____________________
```

## Problem B

Generate every ordering of the elements.

``` text
Pattern:
____________________
```

## Problem C

Place queens so that none attack each other.

``` text
Pattern:
____________________
```

## Problem D

Find a word in a grid without reusing a cell.

``` text
Pattern:
____________________
```

## Problem E

Calculate `n!` using a smaller version of the same problem.

``` text
Pattern:
____________________
```

### Answers

``` text
A → Backtracking
B → Backtracking + used[]
C → Backtracking + pruning
D → Grid Backtracking
E → Recursion
```

# 67. HOMEWORK

### Homework 1

Implement recursively:

``` text
factorial
sum of first n numbers
array traversal
```

### Homework 2

Generate all binary strings of length `n`.

### Homework 3

Solve Subsets without looking at the solution.

### Homework 4

Solve Permutations using `used[]`.

### Homework 5

Solve Combination Sum and explain:

> Why is the recursive index `i` instead of `i + 1`?

### Homework 6

Attempt Generate Parentheses.

Before coding, write:

``` text
state =
choices =
validity =
base case =
undo =
```

### Homework 7

Explain N-Queens without coding it completely.

Write:

``` text
state =
choices =
invalid condition =
pruning =
undo =
```

# 68. QUICK REVISION

## Recursion

``` text
Base case
+
Smaller recursive problem
```

## Call Stack

``` text
Call
 ↓
Call
  ↓
Base
  ↑
Return
 ↑
Return
```

## Backtracking

``` text
Choose
 ↓
Explore
 ↓
Undo
```

## Subsets

``` text
Include / Exclude
```

Count:

``` text
2^n
```

## Permutations

``` text
Choose unused
```

Count:

``` text
n!
```

## Combinations

``` text
Move forward with start index
```

## Combination Sum

``` text
Reuse allowed
→ recurse with i
```

## Grid Backtracking

``` text
Mark
Explore
Restore
```

## N-Queens

``` text
Row
+
Column
+
Diagonal
+
Backtracking
```

# 69. GOLDEN RULES

> **Every recursion needs a reachable base case.**

> **Every recursive call should move toward the base case.**

> **Backtracking = Choose → Explore → Undo.**

> **Subsets → include/exclude.**

> **Permutations → choose unused.**

> **Combinations → move forward with the start index.**

> **Reuse allowed → usually recurse with `i`.**

> **No reuse → usually recurse with `i + 1`.**

> **Invalid branch → prune immediately.**

> **Mutable path → copy before storing.**

> **Grid backtracking → mark, explore, restore.**

# 70. DAY COMPLETION CHECKLIST

``` text
☐ I understand recursion
☐ I understand base case
☐ I understand recursive case
☐ I can trace the call stack
☐ I understand the return phase
☐ I can write factorial recursively
☐ I can recursively traverse an array
☐ I understand recursion space complexity
☐ I understand why naive Fibonacci is slow
☐ I understand backtracking
☐ I know Choose → Explore → Undo
☐ I can generate subsets
☐ I understand 2^n subsets
☐ I can generate permutations
☐ I understand n! permutations
☐ I can generate combinations
☐ I understand start-index control
☐ I understand reuse vs no reuse
☐ I understand Combination Sum
☐ I understand pruning
☐ I understand Generate Parentheses
☐ I understand grid backtracking
☐ I understand N-Queens
☐ I understand state restoration
☐ I completed the daily test
☐ I completed the pattern recognition test
☐ I completed the homework
☐ I solved the introductory practice
☐ I attempted at least 2 Medium problems


# 71. PRACTICE PROBLEMS

The following are verified LeetCode practice targets for today's patterns.

## Easy / Introductory

### 1. Fibonacci Number
Platform: LeetCode  
Difficulty: Easy  
Pattern: Recursion / introductory recursion  
Why: Learn base cases and recursive definitions.  
Practice: https://leetcode.com/problems/fibonacci-number/

### 2. Power of Two
Platform: LeetCode  
Difficulty: Easy  
Pattern: Recursion / divide by 2  
Why: Practice recursive reduction.  
Practice: https://leetcode.com/problems/power-of-two/

## Medium

### 3. Subsets
Pattern: Backtracking  
Why: Learn include/skip and path state.  
Practice: https://leetcode.com/problems/subsets/

### 4. Permutations
Pattern: Backtracking + used array  
Why: Learn order-sensitive branching.  
Practice: https://leetcode.com/problems/permutations/

### 5. Combination Sum
Pattern: Backtracking + reusable choices  
Why: Learn target state and `i` vs `i+1`.  
Practice: https://leetcode.com/problems/combination-sum/

### 6. Letter Combinations of a Phone Number
Pattern: Backtracking  
Why: One choice per digit.  
Practice: https://leetcode.com/problems/letter-combinations-of-a-phone-number/

### 7. Generate Parentheses
Pattern: Backtracking + pruning  
Why: Learn validity constraints.  
Practice: https://leetcode.com/problems/generate-parentheses/

### 8. Word Search
Pattern: Grid backtracking  
Why: Learn visited state and restoration.  
Practice: https://leetcode.com/problems/word-search/

## Hard / Challenge

### 9. N-Queens
Pattern: Backtracking + pruning  
Why: Learn constraint checking and state compression.  
Practice: https://leetcode.com/problems/n-queens/

### 10. Pow(x, n)
Pattern: Divide and conquer / fast exponentiation  
Why: Connect recursion with logarithmic reduction rather than repeated multiplication.  
Practice: https://leetcode.com/problems/powx-n/

### Practice order

```text
Fibonacci
↓
Power of Two
↓
Subsets
↓
Permutations
↓
Combination Sum
↓
Letter Combinations
↓
Generate Parentheses
↓
Word Search
↓
N-Queens
↓
Pow(x,n)
```

# 72. CONSTRAINT THINKING + FINAL AUDIT

Before coding any recursion/backtracking problem, write these five
things:

``` text
1. State
2. Choices
3. Base case
4. Invalid/pruning condition
5. Undo operation
```

Then estimate:

``` text
branching factor
×
recursion depth
```

For generated output, also consider:

``` text
cost of copying each answer
```

### Final self-check

If you cannot explain:

``` text
Why do I recurse?
What does one recursion level represent?
What choices exist?
When do I stop?
What do I undo?
```

do not start coding yet.

------------------------------------------------------------------------

# 73. NAVIGATION

**Previous:** [Day 7 --- Sorting + Binary
Search](Day-07-Sorting-Binary-Search.md)

**Next:** [Day 9 --- Linked List + Stack +
Queue](Day-09-LinkedList-Stack-Queue.md)

**Course:** Java DSA Placement Preparation

------------------------------------------------------------------------

# 🎯 DAY 8 COMPLETE

Your mental model should now be:

``` text
RECURSION
    ↓
Base case
Recursive case
Call stack

BACKTRACKING
    ↓
State
Choices
Choose
Explore
Undo
Prune

CLASSIC PATTERNS
    ↓
Subsets
Permutations
Combinations
Combination Sum
Parentheses
Grid Search
N-Queens
```

**Do not move to Day 9 until you can identify the state, choices, base
case, pruning condition, and undo operation before writing a
backtracking solution.**
