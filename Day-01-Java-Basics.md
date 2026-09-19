# 🔥 DAY 1 — JAVA BASICS FOR DSA

> **Goal:** Build the Java foundation required to start solving DSA problems confidently.
>
> **Priority:** 🔥 MUST KNOW  
> **Estimated Study Time:** 3–4 hours  
> **Recommended split:** 70% problem solving → 20% concepts → 10% revision

---

## 🎯 Today's Goal

By the end of Day 1, you should be able to:

- Understand the basic structure of a Java program.
- Declare and use variables and data types.
- Read input and print output.
- Use arithmetic, relational, logical, and assignment operators.
- Write `if`, `else if`, and `else` conditions.
- Write `for`, `while`, and `do-while` loops.
- Use `break` and `continue`.
- Work with arrays and basic strings.
- Write simple methods/functions.
- Understand `String` vs `StringBuilder` at a basic DSA level.
- Calculate basic time and space complexity for simple code.
- Convert a problem statement into:
  **Input → Observation → Approach → Algorithm → Code → Output**.
- Recognize when a simple loop/condition is the correct pattern.

---

## 📌 Prerequisites

No previous DSA knowledge is required.

You only need:

- Basic computer usage.
- Willingness to trace code line by line.
- Patience to solve small problems before moving to LeetCode.

---

# 🔥 Priority

## 🔥 MUST KNOW

These are the Day 1 foundations you should be comfortable with before moving to DSA:

- Variables and data types
- Input/output
- Operators
- Conditions
- Loops
- Arrays
- Strings
- Methods
- Basic complexity
- Dry runs
- Edge cases

### Why this matters

Almost every DSA problem eventually becomes Java code.

If the DSA idea is correct but your Java syntax, loops, indexing, input handling, or data types are wrong, the solution still fails.

---

# 1. 🧑‍🎓 BEGINNER EXPLANATION — WHAT IS JAVA?

Java is a programming language.

For DSA, you can think of Java as the language we use to tell the computer:

```text
Take input
   ↓
Store data
   ↓
Process data
   ↓
Produce output
```

Example:

```text
Input:
5
3 7 2 9 4

Processing:
Add all numbers

Output:
25
```

Java gives us tools such as:

- Variables
- Arrays
- Loops
- Conditions
- Methods
- Classes
- Collections

We will use these tools to implement DSA algorithms.

---

# 2. BASIC JAVA PROGRAM STRUCTURE

A basic Java program can look like this:

```java
import java.util.*;

class Main {

    public static void main(String[] args) {

        System.out.println("Hello World");

    }
}
```

## Understand each part

### `import java.util.*;`

Imports commonly used classes from Java's utility package.

For DSA, this becomes useful later for:

- `ArrayList`
- `HashMap`
- `HashSet`
- `Queue`
- `Deque`
- `PriorityQueue`
- `Arrays`
- `Collections`

You do not need all of them on Day 1.

---

### `class Main`

Java code is written inside a class.

For coding platforms, the class name may be specified by the platform.

---

### `public static void main(String[] args)`

This is the standard entry point of a normal Java program.

For now, remember:

> **Execution of a normal standalone Java program starts from `main`.**

---

### `System.out.println()`

Prints something and moves to the next line.

```java
System.out.println("Hello");
System.out.println("World");
```

Output:

```text
Hello
World
```

---

### `System.out.print()`

Prints without automatically moving to a new line.

```java
System.out.print("Hello ");
System.out.print("World");
```

Output:

```text
Hello World
```

---

# 3. IMPORTANT TERMINOLOGY

| Term | Meaning |
|---|---|
| Variable | Named storage location for a value |
| Data type | Tells Java what kind of value is stored |
| Expression | Combination of values/operators producing a result |
| Statement | An instruction executed by Java |
| Method | Reusable block of code |
| Parameter | Input variable received by a method |
| Return value | Value produced by a method |
| Array | Fixed-size collection of same-type elements |
| Index | Position used to access an array element |
| String | Sequence of characters |
| Iteration | One execution of a loop |

---

# 4. VARIABLES

A variable stores a value.

```java
int age = 21;
```

Think:

```text
age
 ↓
21
```

You can change it:

```java
age = 22;
```

Now:

```text
age
 ↓
22
```

## Basic syntax

```text
dataType variableName = value;
```

Example:

```java
int number = 10;
```

---

# 5. JAVA DATA TYPES

For DSA, these are especially important:

| Type | Example | Typical use |
|---|---|---|
| `int` | `10` | Most integer problems |
| `long` | `10000000000L` | Large integer values |
| `double` | `3.14` | Decimal calculations |
| `char` | `'A'` | Single character |
| `boolean` | `true` | Conditions |
| `String` | `"hello"` | Text |

## Example

```java
int age = 21;
long population = 8000000000L;
double price = 99.5;
char grade = 'A';
boolean passed = true;
String name = "Riya";
```

---

## ⚠️ `int` vs `long`

This matters in coding assessments.

```java
int x = 100000;
```

For values that may exceed the `int` range, use `long`.

```java
long x = 10000000000L;
```

The `L` tells Java that the literal is a `long`.

### Common mistake

```java
long x = 10000000000;
```

This can fail because the numeric literal itself may be treated as an `int` before assignment.

Use:

```java
long x = 10000000000L;
```

---

# 6. 🧑‍🎓 BEGINNER EXPLANATION — INPUT

A common way to read input is `Scanner`.

```java
import java.util.*;

class Main {

    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt();

        System.out.println(n);
    }
}
```

Input:

```text
10
```

Output:

```text
10
```

---

## Reading multiple values

Input:

```text
10 20
```

Code:

```java
int a = sc.nextInt();
int b = sc.nextInt();

System.out.println(a + b);
```

Output:

```text
30
```

---

## Reading a string

```java
String s = sc.next();
```

For:

```text
hello
```

`s` becomes:

```text
"hello"
```

### `next()` vs `nextLine()`

```java
sc.next();
```

Reads one token.

```java
sc.nextLine();
```

Reads the remaining line.

For beginner DSA problems, `next()` is often enough for single-word strings.

---

# 7. OUTPUT

Useful commands:

```java
System.out.println(10);
System.out.print(10);
```

You can combine values:

```java
int a = 10;
int b = 20;

System.out.println("Sum = " + (a + b));
```

Output:

```text
Sum = 30
```

### Important

This:

```java
System.out.println("10" + 20);
```

produces:

```text
1020
```

because `"10"` is a `String`.

---

# 8. OPERATORS

Operators tell Java to perform an operation.

---

## 8.1 Arithmetic Operators

| Operator | Meaning | Example |
|---|---|---|
| `+` | Addition | `a + b` |
| `-` | Subtraction | `a - b` |
| `*` | Multiplication | `a * b` |
| `/` | Division | `a / b` |
| `%` | Remainder | `a % b` |

### Modulo `%`

Extremely important in DSA.

```java
10 % 3
```

Result:

```text
1
```

Because:

```text
10 = 3 × 3 + 1
```

### Common uses

Modulo helps with:

- Even/odd checks
- Divisibility
- Last digit
- Cyclic patterns

Example:

```java
if (n % 2 == 0) {
    System.out.println("Even");
}
```

---

# 9. INTEGER DIVISION

This is a very common beginner mistake.

```java
int a = 5;
int b = 2;

System.out.println(a / b);
```

Output:

```text
2
```

Not:

```text
2.5
```

Because both operands are integers.

To obtain a decimal result:

```java
System.out.println((double) a / b);
```

Output:

```text
2.5
```

---

# 10. RELATIONAL OPERATORS

Used to compare values.

| Operator | Meaning |
|---|---|
| `==` | Equal |
| `!=` | Not equal |
| `>` | Greater than |
| `<` | Less than |
| `>=` | Greater than or equal |
| `<=` | Less than or equal |

Example:

```java
int a = 10;
int b = 20;

System.out.println(a < b);
```

Output:

```text
true
```

---

# 11. `=` VS `==`

This is one of the most important beginner distinctions.

### `=`

Assignment:

```java
int x = 10;
```

Means:

> Store `10` in `x`.

### `==`

Comparison:

```java
x == 10
```

Means:

> Is `x` equal to `10`?

---

# 12. LOGICAL OPERATORS

| Operator | Meaning |
|---|---|
| `&&` | AND |
| `||` | OR |
| `!` | NOT |

Example:

```java
int age = 20;

if (age >= 18 && age <= 60) {
    System.out.println("Valid");
}
```

Both conditions must be true.

---

## `||` OR

```java
if (day == 6 || day == 7) {
    System.out.println("Weekend");
}
```

Only one condition needs to be true.

---

## `!` NOT

```java
boolean active = true;

if (!active) {
    System.out.println("Inactive");
}
```

`!true` becomes `false`.

---

# 13. 🧑‍🎓 BEGINNER EXPLANATION — IF/ELSE

Conditions allow the program to make decisions.

Real life:

```text
If it rains:
    take umbrella
Else:
    don't take umbrella
```

Java:

```java
if (raining) {
    takeUmbrella();
} else {
    doNotTakeUmbrella();
}
```

---

## Basic syntax

```java
if (condition) {

} else {

}
```

Example:

```java
int n = 7;

if (n % 2 == 0) {
    System.out.println("Even");
} else {
    System.out.println("Odd");
}
```

---

# 14. `else if`

Use `else if` when there are multiple possibilities.

```java
int marks = 85;

if (marks >= 90) {
    System.out.println("A");
} else if (marks >= 75) {
    System.out.println("B");
} else if (marks >= 50) {
    System.out.println("C");
} else {
    System.out.println("F");
}
```

Java checks from top to bottom.

---

# 15. 🧠 PATTERN RECOGNITION — CONDITIONS

Think of `if/else` when:

- The output depends on a condition.
- You need to classify a number.
- You need to check divisibility.
- You need to compare values.
- You need different behavior for different cases.

### Keywords / Clues

- "if"
- "otherwise"
- "greater than"
- "less than"
- "divisible by"
- "even or odd"
- "maximum/minimum of two"

### Ask Yourself

1. What condition separates the cases?
2. What should happen if the condition is true?
3. What should happen otherwise?

---

# 16. 🧑‍🎓 BEGINNER EXPLANATION — LOOPS

A loop repeats code.

Suppose you need:

```text
Print 1
Print 2
Print 3
Print 4
Print 5
```

Writing five separate statements is unnecessary.

A loop lets you say:

> Repeat this operation while a condition is satisfied.

---

# 17. FOR LOOP

Basic structure:

```java
for (initialization; condition; update) {

}
```

Example:

```java
for (int i = 1; i <= 5; i++) {
    System.out.println(i);
}
```

Output:

```text
1
2
3
4
5
```

---

## How the loop works

```text
i = 1
 ↓
Is i <= 5?
 ↓ yes
Print i
 ↓
i++
 ↓
Check again
```

Eventually:

```text
i = 6
 ↓
6 <= 5 ? false
 ↓
Stop
```

---

# 18. DRY RUN — FOR LOOP

Code:

```java
for (int i = 1; i <= 3; i++) {
    System.out.println(i);
}
```

| Iteration | `i` | Condition | Output |
|---|---:|---|---|
| 1 | 1 | `1 <= 3` true | 1 |
| 2 | 2 | `2 <= 3` true | 2 |
| 3 | 3 | `3 <= 3` true | 3 |
| 4 | 4 | `4 <= 3` false | Stop |

---

# 19. WHILE LOOP

Use `while` when the repetition depends on a condition.

```java
int i = 1;

while (i <= 5) {
    System.out.println(i);
    i++;
}
```

Output:

```text
1
2
3
4
5
```

### Important

If you forget:

```java
i++;
```

the loop may never terminate.

---

# 20. DO-WHILE LOOP

A `do-while` loop executes its body at least once.

```java
int i = 1;

do {
    System.out.println(i);
    i++;
} while (i <= 5);
```

For most basic DSA problems, `for` and `while` are used more frequently.

---

# 21. FOR VS WHILE VS DO-WHILE

| Loop | Best mental model |
|---|---|
| `for` | Repeat a known/countable number of times |
| `while` | Repeat while a condition remains true |
| `do-while` | Execute once, then decide whether to continue |

Do not memorize this as a strict rule. Any loop can sometimes implement the same logic.

---

# 22. BREAK

`break` immediately exits the loop.

```java
for (int i = 1; i <= 10; i++) {

    if (i == 5) {
        break;
    }

    System.out.println(i);
}
```

Output:

```text
1
2
3
4
```

---

# 23. CONTINUE

`continue` skips the current iteration.

```java
for (int i = 1; i <= 5; i++) {

    if (i == 3) {
        continue;
    }

    System.out.println(i);
}
```

Output:

```text
1
2
4
5
```

---

# 24. NESTED LOOPS

A loop inside another loop is a nested loop.

```java
for (int i = 1; i <= 3; i++) {

    for (int j = 1; j <= 2; j++) {
        System.out.println(i + " " + j);
    }
}
```

Output:

```text
1 1
1 2
2 1
2 2
3 1
3 2
```

The inner loop runs completely for every outer-loop iteration.

---

# 25. COMPLEXITY OF LOOPS

If:

```java
for (int i = 0; i < n; i++) {
    System.out.println(i);
}
```

There are approximately `n` iterations.

```text
Time: O(n)
Space: O(1)
```

Why?

- Time grows linearly with `n`.
- Only a constant amount of extra memory is used.

---

## Nested loop

```java
for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j++) {
        System.out.println(i + j);
    }
}
```

Approximately:

```text
n × n = n²
```

Therefore:

```text
Time: O(n²)
Space: O(1)
```

---

# 26. 🧠 PATTERN RECOGNITION — LOOPS

Think about a loop when:

- You need to process every number.
- You need to inspect every character.
- You need to repeat an operation.
- You need to count something.
- You need to generate values from `1` to `n`.

### Keywords / Clues

- "for every"
- "from 1 to n"
- "repeat"
- "count"
- "each element"
- "until"
- "while"

### Ask Yourself

1. What is changing every iteration?
2. What is the stopping condition?
3. How many times can the loop run?

---

# 27. 🧑‍🎓 BEGINNER EXPLANATION — ARRAYS

An array stores multiple values of the same type.

Example:

```java
int[] nums = {10, 20, 30, 40};
```

Visualize it as:

```text
Index:   0    1    2    3
        --------------------
Value:  10   20   30   40
```

The first index is `0`.

The last index is:

```text
length - 1
```

For four elements:

```text
last index = 4 - 1 = 3
```

---

# 28. ARRAY CREATION

```java
int[] nums = new int[5];
```

This creates space for five integers.

Initially:

```text
[0, 0, 0, 0, 0]
```

Assign values:

```java
nums[0] = 10;
nums[1] = 20;
```

Now:

```text
[10, 20, 0, 0, 0]
```

---

# 29. ARRAY ACCESS

```java
System.out.println(nums[0]);
```

Gets the first element.

```java
System.out.println(nums[nums.length - 1]);
```

Gets the last element.

---

# 30. ARRAY TRAVERSAL

The standard pattern:

```java
for (int i = 0; i < nums.length; i++) {
    System.out.println(nums[i]);
}
```

Visual:

```text
[10, 20, 30, 40]
 ↑
 i = 0

[10, 20, 30, 40]
      ↑
      i = 1

[10, 20, 30, 40]
           ↑
           i = 2

[10, 20, 30, 40]
                ↑
                i = 3
```

---

# 31. ENHANCED FOR LOOP

You can also write:

```java
for (int x : nums) {
    System.out.println(x);
}
```

Read this as:

> For every value `x` in `nums`, execute the body.

This is convenient when you need values but do not need indices.

---

## When normal `for` is better

Use:

```java
for (int i = 0; i < nums.length; i++)
```

when you need:

- Index
- Previous/next element
- Position-based logic
- Two-pointer movement

---

# 32. ARRAY EDGE CASES

Always consider:

```text
[]
```

or, depending on the problem constraints, an array of size `1`.

For:

```java
int[] nums = {5};
```

Only valid index:

```text
0
```

Trying:

```java
nums[1]
```

causes an `ArrayIndexOutOfBoundsException`.

---

# 33. 🧠 ARRAY PATTERN RECOGNITION

Think about simple array traversal when:

- You must inspect every element.
- You need a sum/count.
- You need maximum/minimum.
- You need to search for a value.
- You need to modify elements.

### Keywords / Clues

- "given an array"
- "find maximum"
- "find minimum"
- "count"
- "sum"
- "search"
- "each element"

### Ask Yourself

1. Do I need to inspect every element?
2. Do I need the index?
3. Can I solve it in one pass?

---

# 34. 🧑‍🎓 BEGINNER EXPLANATION — STRINGS

A `String` represents text.

```java
String s = "hello";
```

Visual:

```text
Index:  0 1 2 3 4
        ---------
Char:   h e l l o
```

Access a character:

```java
char ch = s.charAt(0);
```

Result:

```text
'h'
```

Length:

```java
s.length()
```

---

# 35. STRING TRAVERSAL

```java
String s = "hello";

for (int i = 0; i < s.length(); i++) {
    System.out.println(s.charAt(i));
}
```

Output:

```text
h
e
l
l
o
```

---

# 36. IMPORTANT STRING METHODS

| Method | Purpose |
|---|---|
| `length()` | Number of characters |
| `charAt(i)` | Character at index `i` |
| `equals()` | Compare string contents |
| `substring()` | Extract part of a string |
| `toCharArray()` | Convert to character array |
| `String.valueOf()` | Convert value to String |

Example:

```java
String s = "hello";

System.out.println(s.length());       // 5
System.out.println(s.charAt(1));      // e
System.out.println(s.equals("hello")); // true
```

---

# 37. `==` VS `.equals()` FOR STRINGS

For content comparison, use:

```java
s1.equals(s2)
```

Example:

```java
String a = "hello";
String b = "hello";

if (a.equals(b)) {
    System.out.println("Same");
}
```

For beginner DSA:

> **Use `.equals()` when comparing String contents.**

---

# 38. STRING IS IMMUTABLE

A Java `String` cannot be modified in place.

For example:

```java
String s = "abc";
s = s + "d";
```

A new string value is created.

This becomes important when repeatedly changing strings.

---

# 39. STRINGBUILDER

For repeated string modifications, `StringBuilder` is often useful.

```java
StringBuilder sb = new StringBuilder();

sb.append("a");
sb.append("b");
sb.append("c");

System.out.println(sb.toString());
```

Output:

```text
abc
```

Reverse:

```java
sb.reverse();
```

---

## Why StringBuilder?

Suppose you repeatedly do:

```java
s = s + "x";
```

Many intermediate `String` objects can be created.

`StringBuilder` is designed for efficient mutable string construction.

---

# 40. 🧠 30-SECOND REVISION — STRINGS

```text
String
↓
Sequence of characters

s.length()
↓
Number of characters

s.charAt(i)
↓
Character at index i

s.equals(t)
↓
Content comparison

StringBuilder
↓
Efficient repeated modifications
```

---

# 41. METHODS / FUNCTIONS

A method is a reusable block of code.

Example:

```java
static int add(int a, int b) {
    return a + b;
}
```

Call it:

```java
int result = add(3, 5);
System.out.println(result);
```

Output:

```text
8
```

---

# 42. METHOD TERMINOLOGY

```java
static int add(int a, int b) {
    return a + b;
}
```

| Part | Meaning |
|---|---|
| `static` | Can be called from static context such as `main` |
| `int` | Return type |
| `add` | Method name |
| `int a, int b` | Parameters |
| `return a + b` | Returned result |

---

# 43. VOID METHODS

A method may return nothing.

```java
static void printHello() {
    System.out.println("Hello");
}
```

Call:

```java
printHello();
```

---

# 44. WHY METHODS MATTER IN DSA

Methods help us:

- Organize code.
- Reuse logic.
- Match LeetCode function signatures.
- Test individual pieces.
- Explain an algorithm clearly.

LeetCode often gives:

```java
class Solution {
    public int solve(int[] nums) {

        // solution

    }
}
```

You normally implement the required method rather than writing your own `main`.

---

# 45. JAVA TEMPLATE — BASIC DSA

```java
import java.util.*;

class Main {

    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt();

        // Solve here
    }
}
```

---

# 46. JAVA TEMPLATE — LEETCODE

```java
class Solution {

    public int solve(int[] nums) {

        // solution

        return 0;
    }
}
```

The exact return type and method name depend on the problem.

---

# 47. BRUTE FORCE → OPTIMAL THINKING

Day 1 is not about advanced patterns yet.

But you should learn the mindset now.

Use this process:

```text
Understand the problem
        ↓
Write the simplest correct solution
        ↓
Check constraints
        ↓
Find the bottleneck
        ↓
Look for an optimization
        ↓
Implement
        ↓
Dry run
        ↓
Check edge cases
        ↓
Calculate complexity
```

Do not jump directly to "optimal" code if you do not understand the problem.

---

# 48. EXAMPLE 1 — VERY EASY: SUM OF TWO NUMBERS

## Problem

Given two integers, return their sum.

### Input

```text
a = 10
b = 20
```

### Output

```text
30
```

---

## Observation

Addition is directly available using `+`.

No loop or data structure is required.

---

## Algorithm

```text
1. Read a.
2. Read b.
3. Calculate a + b.
4. Return/print the result.
```

---

## Java

```java
import java.util.*;

class Main {

    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        int a = sc.nextInt();
        int b = sc.nextInt();

        int sum = a + b;

        System.out.println(sum);
    }
}
```

---

## Dry Run

Input:

```text
10 20
```

```text
a = 10
b = 20

sum = 10 + 20
    = 30
```

Output:

```text
30
```

### Complexity

```text
Time: O(1)
Space: O(1)
```

Why?

There is one fixed calculation regardless of input size.

---

## ⚠️ Edge Cases

1. Both numbers are zero.
2. One or both numbers are negative.
3. Values are large enough that `int` may overflow; use `long` if constraints require it.

---

# 49. EXAMPLE 2 — EASY: EVEN OR ODD

## Problem

Determine whether an integer is even or odd.

### Observation

An even number leaves remainder `0` when divided by `2`.

```text
n % 2 == 0
```

---

## Algorithm

```text
1. Read n.
2. Calculate n % 2.
3. If it is 0 → Even.
4. Otherwise → Odd.
```

---

## Java

```java
import java.util.*;

class Main {

    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt();

        if (n % 2 == 0) {
            System.out.println("Even");
        } else {
            System.out.println("Odd");
        }
    }
}
```

---

## Dry Run

Input:

```text
7
```

```text
7 % 2 = 1
```

Therefore:

```text
Odd
```

---

## Complexity

```text
Time: O(1)
Space: O(1)
```

---

## ⚠️ Edge Cases

- `0` → even.
- Negative even number such as `-4` → even.
- Negative odd number such as `-5` → odd.

---

# 50. EXAMPLE 3 — MEDIUM-BEGINNER: FIND MAXIMUM IN AN ARRAY

## Problem

Given an array, find the largest element.

Example:

```text
[4, 7, 2, 9, 1]
```

Answer:

```text
9
```

---

## 🐌 Brute Force

One possible beginner approach is to compare many pairs.

For example:

```text
Compare 4 with every other value
Compare 7 with every other value
...
```

This creates unnecessary comparisons.

A better observation exists.

---

## 💡 Key Observation

We only need one variable:

```text
maximum
```

Scan the array once.

Whenever we see a larger value:

```text
maximum = current value
```

---

## 🚀 Optimal Approach

```text
maximum = first element

for every remaining element:
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

Input:

```text
[4, 7, 2, 9, 1]
```

Start:

```text
maximum = 4
```

| `i` | Current | Maximum |
|---:|---:|---:|
| 1 | 7 | 7 |
| 2 | 2 | 7 |
| 3 | 9 | 9 |
| 4 | 1 | 9 |

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

Why?

- We inspect each element once → `O(n)`.
- We store only `maximum` and the loop variable → `O(1)` extra space.

---

## ⚠️ Edge Cases

1. One-element array: `[5]`.
2. All values equal: `[7,7,7]`.
3. All values negative: `[-5,-2,-9]`.
4. Do not initialize maximum to `0` because an all-negative array would give the wrong result.

---

# 51. EXAMPLE 4 — INTERVIEW STYLE: FIZZ BUZZ

## Problem

For every number from `1` to `n`:

- Divisible by both 3 and 5 → `"FizzBuzz"`
- Divisible by 3 → `"Fizz"`
- Divisible by 5 → `"Buzz"`
- Otherwise → number

For `n = 15`:

```text
1
2
Fizz
4
Buzz
Fizz
7
8
Fizz
Buzz
11
Fizz
13
14
FizzBuzz
```

This is a real LeetCode problem (412, Easy). citeturn0search2

---

## 🧠 Key Observation

Check the most specific condition first:

```text
divisible by both
```

because a number divisible by both 3 and 5 is also divisible by 3 and by 5.

For example:

```text
15 % 3 == 0
15 % 5 == 0
```

Therefore it must produce:

```text
FizzBuzz
```

---

## Java

```java
import java.util.*;

class Solution {

    public List<String> fizzBuzz(int n) {

        List<String> answer = new ArrayList<>();

        for (int i = 1; i <= n; i++) {

            if (i % 3 == 0 && i % 5 == 0) {
                answer.add("FizzBuzz");
            } else if (i % 3 == 0) {
                answer.add("Fizz");
            } else if (i % 5 == 0) {
                answer.add("Buzz");
            } else {
                answer.add(String.valueOf(i));
            }
        }

        return answer;
    }
}
```

---

## Dry Run

For:

```text
n = 15
```

Important iterations:

```text
i = 3
3 % 3 = 0
3 % 5 != 0
→ Fizz

i = 5
5 % 3 != 0
5 % 5 = 0
→ Buzz

i = 15
15 % 3 = 0
15 % 5 = 0
→ FizzBuzz
```

---

## Complexity

```text
Time: O(n)
Space: O(n)
```

Why?

We process `n` numbers.

The returned list contains `n` strings, so output storage is `O(n)`.

---

# 52. 🧠 HOW TO RECOGNIZE BASIC SIMULATION

Think about simple simulation/loop logic when the problem says:

- "For every number from 1 to n..."
- "Print..."
- "Return..."
- "If this condition..."
- "Otherwise..."
- "Process each element..."
- "Count how many..."

### Ask Yourself

1. What are the inputs?
2. What operation happens for one item?
3. Do I repeat that operation?
4. What condition changes the output?
5. Can I process everything in one pass?

---

# 53. 🐌 BRUTE FORCE VS 🚀 ONE-PASS SCANNING

For many beginner problems, the optimization is simply recognizing that repeated work is unnecessary.

Example: maximum element.

### Brute-force mindset

```text
Compare many pairs
```

### Better mindset

```text
Maintain current best
        ↓
Scan once
        ↓
Update when necessary
```

This idea becomes extremely important later in:

- Prefix Sum
- Hashing
- Two Pointers
- Sliding Window
- Greedy algorithms

---

# 54. JAVA-SPECIFIC DSA NOTES

## Arrays

```java
int[] arr = new int[5];
```

Length:

```java
arr.length
```

Important:

```text
Array length → arr.length
String length → s.length()
```

---

## ArrayList

Not a Day 1 core data structure, but you should recognize it.

```java
ArrayList<Integer> list = new ArrayList<>();
```

Add:

```java
list.add(10);
```

Get:

```java
list.get(0);
```

Size:

```java
list.size();
```

Remove:

```java
list.remove(0);
```

---

## HashMap / HashSet

You do not need to master them today.

Just know:

```text
HashMap → key-value mapping
HashSet → unique values
```

They become major topics later.

---

## Stack / Deque

You will later use:

```java
Deque<Integer> stack = new ArrayDeque<>();
```

Do not worry about this today.

---

## Queue

Later:

```java
Queue<Integer> queue = new ArrayDeque<>();
```

---

## PriorityQueue

Later:

```java
PriorityQueue<Integer> pq = new PriorityQueue<>();
```

---

## Sorting

Later you will frequently use:

```java
Arrays.sort(arr);
```

and:

```java
Collections.sort(list);
```

---

# 55. ⚠️ COMMON BEGINNER MISTAKES

## Mistake 1 — Off-by-one loop

Wrong:

```java
for (int i = 0; i <= arr.length; i++)
```

Correct:

```java
for (int i = 0; i < arr.length; i++)
```

Why?

For an array of length `5`, valid indices are:

```text
0 1 2 3 4
```

Not `5`.

---

## Mistake 2 — Confusing `=` and `==`

Wrong:

```java
if (x = 5)
```

Correct:

```java
if (x == 5)
```

---

## Mistake 3 — String comparison with `==`

Avoid:

```java
if (a == b)
```

Use:

```java
if (a.equals(b))
```

when comparing contents.

---

## Mistake 4 — Integer division

```java
5 / 2
```

is:

```text
2
```

not `2.5`.

---

## Mistake 5 — Forgetting loop update

```java
while (i < n) {
    System.out.println(i);
}
```

If `i` never changes, the loop may never terminate.

---

## Mistake 6 — Wrong maximum initialization

Wrong for arbitrary integers:

```java
int max = 0;
```

For:

```text
[-10, -3, -7]
```

this incorrectly gives `0`.

Better:

```java
int max = nums[0];
```

assuming the array is non-empty.

---

## Mistake 7 — Integer overflow

This can overflow:

```java
int product = a * b;
```

when values are large.

Check the constraints and use `long` where needed.

---

## Mistake 8 — Writing complicated code too early

Do not try to impress the compiler.

Prefer:

```java
if (x > max) {
    max = x;
}
```

over unnecessarily clever expressions.

---

# 56. 📊 BASIC CONSTRAINT → ALGORITHM THINKING

These are rough guidelines, not absolute rules.

| Approximate `n` | Often consider |
|---:|---|
| `n <= 20` | Backtracking / exponential may be possible |
| `n <= 100` | `O(n²)` may be possible |
| `n <= 1,000` | `O(n²)` may sometimes be possible |
| `n <= 100,000` | Usually `O(n log n)` or `O(n)` |
| `n <= 1,000,000` | Usually seek `O(n)` or close |
| Very large `n` | Look carefully for logarithmic/constant-time structure |

### Important

Do not blindly select an algorithm from `n`.

Also consider:

- Number of test cases
- Actual operation cost
- Memory limit
- Input structure
- Whether sorting is required
- Whether the problem has special properties

---

# 57. COMPLEXITY CHEAT SHEET — DAY 1

| Code pattern | Typical complexity |
|---|---|
| One calculation | `O(1)` |
| One loop over `n` | `O(n)` |
| Two independent loops over `n` | `O(n)` |
| Nested `n × n` loops | `O(n²)` |
| Array access `arr[i]` | `O(1)` |
| String `charAt(i)` | `O(1)` |
| Scan entire string | `O(n)` |
| Scan array and store constant variables | `O(n)` time, `O(1)` extra space |

### Important distinction

If an algorithm returns an array/list of size `n`, its **output space** can be `O(n)`.

When discussing auxiliary space, some interviewers exclude the required output.

State your convention when it matters.

---

# 58. 🧠 PATTERN COMPARISON — ARRAY VS STRING

| Feature | Array | String |
|---|---|---|
| Stores | Elements of a type | Characters |
| Access | `arr[i]` | `s.charAt(i)` |
| Length | `arr.length` | `s.length()` |
| Mutable? | Yes | No, `String` is immutable |
| Common traversal | `for` loop | `for` + `charAt()` |
| Useful mutable text tool | — | `StringBuilder` |

---

# 59. 🧠 PATTERN COMPARISON — FOR VS WHILE

| Feature | `for` | `while` |
|---|---|---|
| Initialization | Usually in loop header | Usually before loop |
| Update | Usually in loop header | Usually inside body |
| Best for | Count-controlled repetition | Condition-controlled repetition |
| DSA usage | Very common | Very common |

Neither is automatically faster. Choose the form that makes the logic easiest to understand.

---

# 60. 🎤 HOW TO EXPLAIN BASIC LOOP PROBLEMS IN AN INTERVIEW

You can structure your explanation like this:

> "First, I identify what must be processed. Since every element needs to be checked, I use a single loop."

> "For each element, I apply the required condition or update."

> "I maintain only the necessary variables, so the extra space is constant."

> "Because each element is processed once, the time complexity is O(n), and the auxiliary space is O(1)."

For a condition-only problem:

> "The key observation is that the required classification can be determined directly using the condition, so no additional data structure is needed."

---

# 61. 🧪 TRY YOURSELF — MINI PRACTICE

Do these **before opening the solutions**.

## Problem 1

Given an integer `n`, print all numbers from `1` to `n`.

Example:

```text
Input: 5
Output:
1
2
3
4
5
```

<details>
<summary>💡 Hint</summary>

Use a `for` loop.

</details>

<details>
<summary>✅ Solution</summary>

### Approach

Start at `1` and continue while `i <= n`.

```java
for (int i = 1; i <= n; i++) {
    System.out.println(i);
}
```

### Complexity

```text
Time: O(n)
Space: O(1)
```

### Dry Run

For `n = 3`:

```text
i = 1 → print 1
i = 2 → print 2
i = 3 → print 3
i = 4 → stop
```

### Edge Cases

- `n = 1`
- Very large `n`

</details>

---

## Problem 2

Given an integer `n`, count how many even numbers exist from `1` to `n`.

Example:

```text
Input: 10
Output: 5
```

<details>
<summary>💡 Hint</summary>

Loop from `1` to `n` and check:

```java
i % 2 == 0
```

</details>

<details>
<summary>✅ Solution</summary>

```java
int count = 0;

for (int i = 1; i <= n; i++) {

    if (i % 2 == 0) {
        count++;
    }
}

System.out.println(count);
```

### Complexity

```text
Time: O(n)
Space: O(1)
```

</details>

---

# 62. 🧪 MINI PRACTICE — ARRAY

## Problem 1

Find the sum of all elements.

```text
[2, 4, 6, 8]
```

<details>
<summary>💡 Hint</summary>

Maintain a variable called `sum`.

</details>

<details>
<summary>✅ Solution</summary>

```java
int sum = 0;

for (int i = 0; i < nums.length; i++) {
    sum += nums[i];
}

return sum;
```

Complexity:

```text
Time: O(n)
Space: O(1)
```

</details>

---

## Problem 2

Count how many elements are greater than `10`.

```text
[5, 12, 8, 20, 15]
```

<details>
<summary>💡 Hint</summary>

Use a counter and an `if` condition.

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

Complexity:

```text
Time: O(n)
Space: O(1)
```

</details>

---

# 63. 🧪 MINI PRACTICE — STRING

## Problem 1

Count the number of vowels in a string.

Example:

```text
Input: "hello"
Output: 2
```

<details>
<summary>💡 Hint</summary>

For each character, check whether it is one of:

```text
a e i o u
```

</details>

<details>
<summary>✅ Solution</summary>

```java
int count = 0;

for (int i = 0; i < s.length(); i++) {

    char ch = s.charAt(i);

    if (ch == 'a' || ch == 'e' || ch == 'i'
            || ch == 'o' || ch == 'u') {
        count++;
    }
}

return count;
```

Complexity:

```text
Time: O(n)
Space: O(1)
```

</details>

---

## Problem 2

Count the number of uppercase letters in a string.

<details>
<summary>💡 Hint</summary>

You can compare a character with:

```text
'A' to 'Z'
```

</details>

<details>
<summary>✅ Solution</summary>

```java
int count = 0;

for (int i = 0; i < s.length(); i++) {

    char ch = s.charAt(i);

    if (ch >= 'A' && ch <= 'Z') {
        count++;
    }
}

return count;
```

Complexity:

```text
Time: O(n)
Space: O(1)
```

</details>

---

# 64. 🧪 MINI PRACTICE — METHODS

Write a method:

```java
isPositive(int n)
```

that returns `true` when `n > 0`.

<details>
<summary>💡 Hint</summary>

The return type should be `boolean`.

</details>

<details>
<summary>✅ Solution</summary>

```java
static boolean isPositive(int n) {
    return n > 0;
}
```

Complexity:

```text
Time: O(1)
Space: O(1)
```

</details>

---

# 65. PRACTICE PROBLEMS

The problems below are arranged from very easy to slightly more challenging.

## 🟢 Easy

### 1. Solve Me First

**Platform:** HackerRank  
**Difficulty:** Easy  
**Pattern:** Basic arithmetic / function  
**Why this pattern:** Tests basic input, output, function implementation, and addition.  
**What you should notice:** The operation is constant-time.  
**Expected Complexity:** `O(1)` time, `O(1)` space

urlPractice Problem — Solve Me Firstturn0search1

---

### 2. Simple Array Sum

**Platform:** HackerRank  
**Difficulty:** Easy  
**Pattern:** Array traversal  
**Why this pattern:** You must inspect every array element and accumulate a result.  
**What you should notice:** One pass is sufficient.  
**Expected Complexity:** `O(n)` time, `O(1)` auxiliary space

urlPractice Problem — Simple Array Sumturn0search0

---

### 3. Java 1D Array

**Platform:** HackerRank  
**Difficulty:** Easy  
**Pattern:** Array basics  
**Why this pattern:** Reinforces array creation, indexing, storage, and traversal.  
**What you should notice:** Array indices start at `0`.  
**Expected Complexity:** `O(n)` time

urlPractice Problem — Java 1D Arrayturn0search12

---

## 🟡 Medium / Next-Step Foundation

Day 1 should not overload you with advanced problems. Use these as bridge problems after completing the basic exercises.

### 4. Fizz Buzz

**Platform:** LeetCode  
**Difficulty:** Easy  
**Pattern:** Simulation / conditions  
**Why this pattern:** Combines loops, modulo, condition ordering, and output construction.  
**What you should notice:** Check the combined condition before individual conditions.  
**Expected Complexity:** `O(n)` time, `O(n)` output space

urlPractice Problem — Fizz Buzzturn0search2

---

### 5. Intro to Tutorial Challenges

**Platform:** HackerRank  
**Difficulty:** Easy  
**Pattern:** Linear search / array traversal  
**Why this pattern:** Introduces searching through an array and index tracking.  
**What you should notice:** The provided problem guarantees that the target occurs exactly once.  
**Expected Complexity:** `O(n)` time

urlPractice Problem — Intro to Tutorial Challengesturn0search14

---

## 🔴 Hard / Challenge

No hard DSA problem is required for Day 1.

**Reason:** The goal is to build the Java and problem-solving foundation needed before introducing patterns such as hashing, two pointers, binary search, recursion, and sliding window.

---

# 66. PRACTICE ORDER

Follow this order:

```text
1. Solve Me First
        ↓
2. Java 1D Array
        ↓
3. Simple Array Sum
        ↓
4. Fizz Buzz
        ↓
5. Intro to Tutorial Challenges
```

Do not rush into difficult problems.

The objective is not the number of problems completed.

The objective is:

```text
Understand
   ↓
Code independently
   ↓
Dry run
   ↓
Explain complexity
   ↓
Recognize the pattern
```

---

# 67. 🧠 PATTERN RECOGNITION TEST

For each statement, identify the basic technique before writing code.

| Problem statement | Pattern to think about | Why |
|---|---|---|
| Print numbers from 1 to `n` | Loop | Repeated operation |
| Find sum of all array elements | Linear traversal | Every element contributes |
| Find maximum in an array | Linear scan | Maintain current maximum |
| Determine even/odd | Modulo + condition | Divisibility by 2 |
| Count vowels | String traversal + condition | Inspect every character |
| Print Fizz/Buzz based on divisibility | Simulation + conditions | Output depends on each number |
| Find whether a value exists | Linear search | Inspect elements until found |
| Count positive numbers | Traversal + condition | Classify each element |
| Reverse a string using repeated appending | StringBuilder / traversal | Build result efficiently |
| Find the first matching element | Linear search | Stop when target is found |

---

# 68. DAILY QUIZ — 10 QUESTIONS

Try these **without looking at the answer key**.

## Q1 — MCQ

What is the first valid index of a Java array?

A. `1`  
B. `0`  
C. `-1`  
D. Depends on the array

---

## Q2 — Output Prediction

What is printed?

```java
int a = 5;
int b = 2;

System.out.println(a / b);
```

A. `2.5`  
B. `3`  
C. `2`  
D. Compilation error

---

## Q3 — MCQ

Which operator gives the remainder?

A. `/`  
B. `//`  
C. `%`  
D. `rem`

---

## Q4 — Output Prediction

What is printed?

```java
for (int i = 1; i <= 3; i++) {
    System.out.print(i);
}
```

A. `123`  
B. `012`  
C. `1234`  
D. `321`

---

## Q5 — Complexity

What is the time complexity?

```java
for (int i = 0; i < n; i++) {
    System.out.println(i);
}
```

A. `O(1)`  
B. `O(log n)`  
C. `O(n)`  
D. `O(n²)`

---

## Q6 — Debugging

What is wrong here?

```java
int[] arr = {10, 20, 30};

for (int i = 0; i <= arr.length; i++) {
    System.out.println(arr[i]);
}
```

---

## Q7 — Concept

What is the difference between:

```java
=
```

and

```java
==
```

?

---

## Q8 — Pattern Recognition

You are asked:

> "Given an array, find the largest value."

What basic approach should you first consider?

A. Recursion  
B. Linear scan  
C. Graph BFS  
D. Dynamic programming

---

## Q9 — Small Coding

Write one condition that checks whether `n` is even.

---

## Q10 — Output Prediction

What is printed?

```java
String s = "hello";

System.out.println(s.charAt(1));
```

A. `h`  
B. `e`  
C. `l`  
D. `o`

---

# 69. 📝 ANSWER KEY

### Q1

**B. `0`**

Java arrays use zero-based indexing.

---

### Q2

**C. `2`**

Both operands are integers, so integer division is performed.

---

### Q3

**C. `%`**

Modulo returns the remainder.

---

### Q4

**A. `123`**

The loop executes for `i = 1, 2, 3`.

---

### Q5

**C. `O(n)`**

The loop runs approximately `n` times.

---

### Q6

The condition should be:

```java
i < arr.length
```

not:

```java
i <= arr.length
```

For length `3`, valid indices are `0, 1, 2`.

---

### Q7

`=` assigns a value.

```java
x = 5;
```

`==` compares values.

```java
x == 5
```

---

### Q8

**B. Linear scan**

Inspect each element and maintain the largest value.

---

### Q9

```java
n % 2 == 0
```

---

### Q10

**B. `e`**

String indexing starts at `0`:

```text
h → 0
e → 1
l → 2
l → 3
o → 4
```

---

# 70. ⚡ 30-SECOND REVISION

## Java basics

```text
class Main
    ↓
main()
    ↓
read input
    ↓
process
    ↓
print output
```

## Data types

```text
int      → normal integers
long     → larger integers
double   → decimal values
char     → one character
boolean  → true/false
String   → text
```

## Operators

```text
+  -  *  /  %
== != > < >= <=
&& || !
```

## Conditions

```java
if (...) {

} else if (...) {

} else {

}
```

## Loops

```java
for (int i = 0; i < n; i++) {

}
```

```java
while (condition) {

}
```

## Array

```java
int[] arr = {1, 2, 3};

for (int i = 0; i < arr.length; i++) {
    System.out.println(arr[i]);
}
```

## String

```java
s.length()
s.charAt(i)
s.equals(t)
```

## Method

```java
static int add(int a, int b) {
    return a + b;
}
```

---

# 71. 🔁 QUICK REVISION

## Remember These

- Java arrays are **zero-indexed**.
- `arr.length` gives array size.
- `s.length()` gives String length.
- `%` gives the remainder.
- `=` means assignment.
- `==` means comparison.
- Use `.equals()` for String content comparison.
- `int / int` performs integer division.
- Use `long` when constraints can exceed `int`.
- A single loop over `n` items is usually `O(n)`.
- Nested `n × n` loops are usually `O(n²)`.
- Start maximum/minimum from the first element when the input is guaranteed non-empty.
- Always check loop boundaries.
- Always inspect constraints before choosing a data type/algorithm.
- Prefer simple, readable Java code.

---

## Important Templates

### Basic program

```java
import java.util.*;

class Main {

    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        // input

        // logic

        // output
    }
}
```

### Array traversal

```java
for (int i = 0; i < arr.length; i++) {
    int value = arr[i];
}
```

### Enhanced array traversal

```java
for (int value : arr) {
    // use value
}
```

### Condition

```java
if (condition) {

} else {

}
```

### Count

```java
int count = 0;

for (int x : arr) {
    if (condition) {
        count++;
    }
}
```

### Sum

```java
int sum = 0;

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

### String traversal

```java
for (int i = 0; i < s.length(); i++) {
    char ch = s.charAt(i);
}
```

### LeetCode class

```java
class Solution {

    public int solve(int[] nums) {

        // solution

        return 0;
    }
}
```

---

## Complexity Cheat Sheet

| Pattern | Time | Extra Space |
|---|---:|---:|
| Constant calculation | `O(1)` | `O(1)` |
| One loop | `O(n)` | `O(1)` |
| Two independent loops | `O(n)` | `O(1)` |
| Nested loops | `O(n²)` | `O(1)` |
| Array indexing | `O(1)` | `O(1)` |
| Full array traversal | `O(n)` | `O(1)` |
| Full string traversal | `O(n)` | `O(1)` |

---

## Recognition Cheat Sheet

| If you see... | Think... |
|---|---|
| "from 1 to n" | `for` loop |
| "for every element" | Array traversal |
| "count how many" | Counter + condition |
| "sum all" | Running sum |
| "largest/smallest" | Running maximum/minimum |
| "even/odd" | `% 2` |
| "divisible by" | `%` |
| "each character" | String traversal |
| "first occurrence" | Linear scan + early stop |
| "different output depending on condition" | `if/else` |
| "build a string repeatedly" | `StringBuilder` |

---

# 72. 🏠 HOMEWORK

## Must Solve

1. HackerRank — **Solve Me First**
2. HackerRank — **Java 1D Array**
3. HackerRank — **Simple Array Sum**
4. LeetCode — **Fizz Buzz**

## Must Write Yourself Without Looking

5. Find the maximum element of an array.
6. Find the minimum element of an array.
7. Count even numbers in an array.
8. Count vowels in a string.

## Optional Challenge

9. Reverse a string using `StringBuilder`.
10. Check whether a number is a palindrome **using only basic loops and arithmetic**.

### Homework rule

For every problem, write down:

```text
1. Input
2. Output
3. Observation
4. Approach
5. Code
6. Dry run
7. Time complexity
8. Space complexity
9. Edge cases
```

---

# 73. DAY-END SELF TEST

Before moving to Day 2, close this file and try to answer:

```text
Can I write a Java program from scratch?
Can I read an integer?
Can I read a String?
Can I use if/else?
Can I write a for loop?
Can I write a while loop?
Can I traverse an array?
Can I traverse a String?
Can I write a method?
Can I explain O(1), O(n), and O(n²)?
Can I dry-run my own code?
Can I identify basic edge cases?
```

If you cannot answer some of these yet, repeat the relevant section rather than rushing forward.

---

# ✅ DAY COMPLETION CHECKLIST

- [ ] I understand the basic concept
- [ ] I can explain it without notes
- [ ] I can identify the pattern
- [ ] I can implement the basic Java template
- [ ] I understand brute force
- [ ] I understand optimization
- [ ] I know the complexity
- [ ] I know common edge cases
- [ ] I solved the easy problems
- [ ] I attempted the medium problems
- [ ] I completed the quiz
- [ ] I can write a Java program without copying the template
- [ ] I can dry-run a loop manually
- [ ] I can traverse an array
- [ ] I can traverse a String
- [ ] I can explain why an algorithm is `O(n)`

---

# 🚦 READY FOR DAY 2?

Move forward only when the Day 1 basics feel comfortable.

Next:

➡️ [Day 2 — Number Problems + Patterns](Day-02-Number-Problems-Patterns.md)

⬅️ [Previous Day](#)  
➡️ [Next Day — Number Problems + Patterns](Day-02-Number-Problems-Patterns.md)

---

# 📌 SOURCE / LINK VERIFICATION NOTE

The external practice links included in this file were checked against current search results. The HackerRank pages identify **Solve Me First**, **Simple Array Sum**, **Java 1D Array**, and **Intro to Tutorial Challenges** as the corresponding challenges; LeetCode's page identifies **Fizz Buzz** as problem 412. 

The exact URLs are intentionally linked through the verified source references rather than guessed generic homepages.

---

# 🎯 FINAL DAY 1 MINDSET

Do not try to memorize Java syntax line by line.

Instead, build this mental flow:

```text
PROBLEM
   ↓
What is the input?
   ↓
What is the output?
   ↓
What changes?
   ↓
Can I solve it with a condition?
   ↓
Can I solve it with one loop?
   ↓
Do I need an array/string?
   ↓
Can I avoid repeated work?
   ↓
Write simple Java
   ↓
Dry run
   ↓
Check edge cases
   ↓
Calculate complexity
```

The goal of Day 1 is not to become an advanced DSA programmer.

The goal is to become comfortable enough with Java that **Java syntax stops being the main obstacle when DSA starts**.

---

**End of Day 1**
