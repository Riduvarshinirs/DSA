# Java DSA – Pattern Printing Notes

## 1. PATTERN PRINTING — THE CORE IDEA

Consider:

```text
* * *
* * *
* * *
```

There are:

```text
3 rows
3 stars in every row
```

Therefore:

```java
for (int row = 1; row <= 3; row++) {

    for (int col = 1; col <= 3; col++) {
        System.out.print("* ");
    }

    System.out.println();
}
```

### Mental Model

```text
row 1 → * * *
row 2 → * * *
row 3 → * * *
```

The outer loop controls **which row** you're currently printing.

The inner loop controls **what goes inside that row**.

### 🔥 Remember This Permanently

> **Outer loop = rows**  
> **Inner loop = columns/items**

---

# 2. SQUARE

### Problem

> Print an N × N square.

For `N = 4`:

```text
****
****
****
****
```

### Think First

```text
Rows = 4
Stars per row = 4
```

Therefore:

```java
for (int row = 1; row <= n; row++) {

    for (int col = 1; col <= n; col++) {
        System.out.print("*");
    }

    System.out.println();
}
```

### Pattern

```text
n rows
n columns
```

### Complexity

There are `n × n` stars.

- **Time:** `O(n²)`
- **Space:** `O(1)`

---

# 3. RECTANGLE

Suppose:

```text
rows = 3
columns = 5
```

Output:

```text
*****
*****
*****
```

Code:

```java
for (int row = 1; row <= rows; row++) {

    for (int col = 1; col <= cols; col++) {
        System.out.print("*");
    }

    System.out.println();
}
```

Notice:

```text
Outer → rows
Inner → columns
```

---

# 4. RIGHT TRIANGLE ⭐

Output:

```text
*
**
***
****
*****
```

For each row, the number of stars changes.

Look carefully:

| Row | Stars |
|---:|---:|
| 1 | 1 |
| 2 | 2 |
| 3 | 3 |
| 4 | 4 |
| 5 | 5 |

Therefore:

> **Stars = row number**

So:

```java
for (int row = 1; row <= n; row++) {

    for (int col = 1; col <= row; col++) {
        System.out.print("*");
    }

    System.out.println();
}
```

### 🔥 Recognition

Whenever you see:

```text
1 item
2 items
3 items
4 items
...
```

Think:

```java
col <= row
```

---

# 5. INVERTED TRIANGLE

Output:

```text
*****
****
***
**
*
```

Now observe:

| Row | Stars |
|---:|---:|
| 1 | 5 |
| 2 | 4 |
| 3 | 3 |
| 4 | 2 |
| 5 | 1 |

So:

```text
stars = n - row + 1
```

Code:

```java
for (int row = 1; row <= n; row++) {

    for (int col = 1; col <= n - row + 1; col++) {
        System.out.print("*");
    }

    System.out.println();
}
```

### Recognition

Increasing:

```text
1
2
3
4
5
```

→ `col <= row`

Decreasing:

```text
5
4
3
2
1
```

→ `col <= n - row + 1`

---

# 6. NUMBER TRIANGLE

Output:

```text
1
12
123
1234
12345
```

The number of items still follows:

```text
1
2
3
4
5
```

But instead of printing `*`, print `col`.

```java
for (int row = 1; row <= n; row++) {

    for (int col = 1; col <= row; col++) {
        System.out.print(col);
    }

    System.out.println();
}
```

---

# 7. REPEATED NUMBER TRIANGLE

Output:

```text
1
22
333
4444
55555
```

What changes?

The number printed is the **row number**.

Therefore:

```java
for (int row = 1; row <= n; row++) {

    for (int col = 1; col <= row; col++) {
        System.out.print(row);
    }

    System.out.println();
}
```

### Important Distinction

```text
12345
```

uses:

```java
System.out.print(col);
```

while:

```text
11111
22222
33333
```

uses:

```java
System.out.print(row);
```

---

# 8. INCREASING NUMBERS

Output:

```text
1
23
456
78910
```

Now the number doesn't reset at every row.

We need a separate variable:

```java
int num = 1;
```

Then:

```java
for (int row = 1; row <= n; row++) {

    for (int col = 1; col <= row; col++) {
        System.out.print(num + " ");
        num++;
    }

    System.out.println();
}
```

### Important Concept

A variable can maintain information **between loop iterations**.

That's the same idea as an accumulator.

---

# 9. 0-1 TRIANGLE ⭐

Output:

```text
1
01
101
0101
10101
```

Look at the relationship between row and column.

A simple observation:

```text
if (row + col) is even → 1
otherwise → 0
```

Code:

```java
for (int row = 1; row <= n; row++) {

    for (int col = 1; col <= row; col++) {

        if ((row + col) % 2 == 0) {
            System.out.print("1");
        } else {
            System.out.print("0");
        }
    }

    System.out.println();
}
```

### Why?

For row 1:

```text
row + col = 1 + 1 = 2 → even → 1
```

Row 2:

```text
2 + 1 = 3 → 0
2 + 2 = 4 → 1
```

Giving:

```text
01
```

### 🔥 Key Lesson

This is a good example of **finding a mathematical relationship between row and column**.

---

# 10. RIGHT-ALIGNED TRIANGLE

Output:

```text
    *
   **
  ***
 ****
*****
```

This is where beginners usually get confused.

Don't immediately think about stars.

First count **spaces**.

For `n = 5`:

```text
row 1 → 4 spaces + 1 star
row 2 → 3 spaces + 2 stars
row 3 → 2 spaces + 3 stars
row 4 → 1 space  + 4 stars
row 5 → 0 spaces + 5 stars
```

So:

```text
spaces = n - row
stars = row
```

Code:

```java
for (int row = 1; row <= n; row++) {

    for (int space = 1; space <= n - row; space++) {
        System.out.print(" ");
    }

    for (int col = 1; col <= row; col++) {
        System.out.print("*");
    }

    System.out.println();
}
```

---

# 🔥 PATTERN FORMULA

For almost every pattern, create this table:

| Row | Spaces | Stars |
|---:|---:|---:|
| 1 | 4 | 1 |
| 2 | 3 | 2 |
| 3 | 2 | 3 |
| 4 | 1 | 4 |
| 5 | 0 | 5 |

Then derive:

```text
spaces = n - row
stars = row
```

This is **much better than memorizing code**.

---

# 11. PYRAMID ⭐

Output:

```text
    *
   ***
  *****
 *******
*********
```

For `n = 5`:

| Row | Spaces | Stars |
|---:|---:|---:|
| 1 | 4 | 1 |
| 2 | 3 | 3 |
| 3 | 2 | 5 |
| 4 | 1 | 7 |
| 5 | 0 | 9 |

Stars:

```text
1
3
5
7
9
```

Formula:

```text
stars = 2 * row - 1
```

Spaces:

```text
spaces = n - row
```

Code:

```java
for (int row = 1; row <= n; row++) {

    for (int space = 1; space <= n - row; space++) {
        System.out.print(" ");
    }

    for (int col = 1; col <= 2 * row - 1; col++) {
        System.out.print("*");
    }

    System.out.println();
}
```

---

# 12. INVERTED PYRAMID

Output:

```text
*********
 *******
  *****
   ***
    *
```

Spaces:

```text
0
1
2
3
4
```

Stars:

```text
9
7
5
3
1
```

Formula:

```text
spaces = row - 1
stars = 2 * (n - row) + 1
```

Code:

```java
for (int row = 1; row <= n; row++) {

    for (int space = 1; space < row; space++) {
        System.out.print(" ");
    }

    for (int col = 1; col <= 2 * (n - row) + 1; col++) {
        System.out.print("*");
    }

    System.out.println();
}
```

---

# 13. DIAMOND

Combine:

```text
Pyramid
+
Inverted Pyramid
```

For example:

```text
  *
 ***
*****
 ***
  *
```

Instead of memorizing an entirely new pattern:

```text
upper half
+
lower half
```

Code:

```java
// Upper half
for (int row = 1; row <= n; row++) {

    for (int space = 1; space <= n - row; space++) {
        System.out.print(" ");
    }

    for (int col = 1; col <= 2 * row - 1; col++) {
        System.out.print("*");
    }

    System.out.println();
}

// Lower half
for (int row = n - 1; row >= 1; row--) {

    for (int space = 1; space <= n - row; space++) {
        System.out.print(" ");
    }

    for (int col = 1; col <= 2 * row - 1; col++) {
        System.out.print("*");
    }

    System.out.println();
}
```

### 🔥 Huge Lesson

> **Complex patterns can often be broken into smaller known patterns.**

---

# 14. HOLLOW SQUARE ⭐

Output:

```text
*****
*   *
*   *
*   *
*****
```

For every position `(row, col)`:

Print `*` if you're on the **boundary**.

Boundary conditions:

```text
row == 1
row == n
col == 1
col == n
```

Otherwise print a space.

```java
for (int row = 1; row <= n; row++) {

    for (int col = 1; col <= n; col++) {

        if (row == 1 || row == n ||
            col == 1 || col == n) {
            System.out.print("*");
        } else {
            System.out.print(" ");
        }
    }

    System.out.println();
}
```

### 🔥 Recognition

Whenever you hear:

> **Hollow**

Think:

> **Print only the boundary.**

This idea will appear again in hollow rectangles, triangles, pyramids, diamonds, etc.

---

# 🧠 PATTERN RECOGNITION CHEAT SHEET

| Output Behavior | Think |
|---|---|
| Same number of items every row | Fixed inner loop |
| `1, 2, 3, 4...` items | `col <= row` |
| `n, n-1, n-2...` items | `col <= n - row + 1` |
| Right aligned | Spaces + items |
| Pyramid | Spaces + `2 * row - 1` |
| Inverted pyramid | Spaces increase + stars decrease |
| Hollow | Boundary condition |
| Number printed changes by row | `row` |
| Number printed changes by column | `col` |
| Continuous numbers | Separate counter variable |
| Diamond | Pyramid + inverted pyramid |

---

# 🚀 HOW TO APPROACH ANY PATTERN PRINTING PROBLEM

Don't memorize the code.

Use this process:

### Step 1 — Count the rows

Ask:

```text
How many rows are there?
```

Usually:

```java
for (int row = 1; row <= n; row++)
```

---

### Step 2 — Count what is inside each row

Ask:

```text
How many stars/numbers/spaces are in each row?
```

Create a table if necessary.

---

### Step 3 — Find the formula

Look for relationships such as:

```text
1, 2, 3, 4, ...
```

→ `row`

```text
n, n-1, n-2, ...
```

→ `n - row + 1`

```text
1, 3, 5, 7, ...
```

→ `2 * row - 1`

```text
4, 3, 2, 1, 0
```

→ `n - row`

---

### Step 4 — Identify what to print

Ask:

```text
Should I print:
* ?
row ?
col ?
num ?
space ?
```

Examples:

```java
System.out.print("*");
```

```java
System.out.print(row);
```

```java
System.out.print(col);
```

```java
System.out.print(num);
```

---

### Step 5 — Check whether the pattern has multiple parts

If yes, split it.

For example:

```text
Diamond
    ↓
Pyramid
+
Inverted Pyramid
```

---

### Step 6 — Check for a condition

For hollow or alternating patterns, use conditions.

Examples:

```java
if (row == 1 || row == n ||
    col == 1 || col == n)
```

or:

```java
if ((row + col) % 2 == 0)
```

---

# 🔥 FINAL MENTAL MODEL

For every pattern, think:

```text
                PATTERN
                   |
          +--------+--------+
          |                 |
        ROWS            CONTENT
          |                 |
     Outer loop        Inner loop
                            |
                    +-------+-------+
                    |       |       |
                  spaces   stars   numbers
```

The most important skill is **not memorizing pattern code**.

The skill is:

> **Look at the output → identify the row behavior → identify the column/content behavior → derive the formula → write the loops.**

Once you can do that, even unfamiliar pattern-printing questions become much easier.
