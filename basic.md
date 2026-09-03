# Java DSA – Basic Logic Revision

A quick revision guide for commonly used Java DSA logic patterns.

---

## 1. Counting

Use when the question asks **how many times** something occurs.

### Basic Logic

```java
count++;
```

### Pattern

```java
int count = 0;

if (condition) {
    count++;
}
```

### Remember

`count++` → increases the count by `1`.

---

## 2. Sum

Use when the question asks for the **total/sum** of values or digits.

### Basic Logic

```java
sum += digit;
```

Same as:

```java
sum = sum + digit;
```

### Pattern

```java
int sum = 0;

sum += digit;
```

### Remember

`sum += digit` → adds the current value to the total.

---

## 3. Maximum

Use when you need to find the **largest value**.

### Basic Logic

```java
max = Math.max(max, digit);
```

### Pattern

```java
int max = Integer.MIN_VALUE;

max = Math.max(max, digit);
```

### How it works

`Math.max(a, b)` returns the larger of `a` and `b`.

### Example

```java
max = Math.max(10, 7);
```

Result:

```text
10
```

### Remember

```java
max = Math.max(max, value);
```

→ Keeps the **largest value seen so far**.

---

## 4. Frequency

Use when you need to find **how many times each value occurs**.

For digits `0–9`:

```java
int[] frequency = new int[10];
```

Then:

```java
frequency[digit]++;
```

### Example

For:

```text
112233
```

Frequency becomes:

```text
0 → 0
1 → 2
2 → 2
3 → 2
```

### Pattern

```java
int[] frequency = new int[10];

for (int digit : arr) {
    frequency[digit]++;
}
```

### Remember

```java
frequency[value]++;
```

→ Increase the count of that particular value.

---

# 5. Prime Number

A prime number has **exactly two factors: 1 and itself**.

### Code

```java
boolean prime = true;

for (int i = 2; i * i <= n; i++) {
    if (n % i == 0) {
        prime = false;
        break;
    }
}
```

### Important Logic

We start checking from:

```java
i = 2;
```

and continue while:

```java
i * i <= n
```

If any number divides `n` exactly:

```java
n % i == 0
```

then `n` is **not prime**.

### Why `i * i <= n`?

We only need to check factors up to `√n`.

For example, if:

```text
n = 25
```

Then:

```text
i = 2 → 25 % 2 != 0
i = 3 → 25 % 3 != 0
i = 4 → 25 % 4 != 0
i = 5 → 25 % 5 == 0
```

Therefore:

```text
25 → Not Prime
```

### Important Edge Cases

```text
0 → Not Prime
1 → Not Prime
2 → Prime
3 → Prime
```

### Why does `n = 2` work?

For:

```text
n = 2
```

The loop starts with:

```text
i = 2
```

Then the condition is checked:

```text
i * i <= n

2 * 2 <= 2

4 <= 2 → false
```

So the loop does **not** execute.

Therefore:

```text
2 → Prime
```

### Remember

```java
for (int i = 2; i * i <= n; i++) {
    if (n % i == 0) {
        prime = false;
        break;
    }
}
```

---

# 6. GCD

**GCD = Greatest Common Divisor**

It finds the largest number that divides both numbers.

### Example

For `12` and `18`:

```text
Factors of 12 → 1, 2, 3, 4, 6, 12
Factors of 18 → 1, 2, 3, 6, 9, 18

GCD = 6
```

### Euclidean Algorithm

```java
static int gcd(int a, int b) {
    while (b != 0) {
        int temp = a % b;
        a = b;
        b = temp;
    }

    return a;
}
```

### Core Logic

First calculate:

```java
a % b
```

Store the remainder:

```java
int temp = a % b;
```

Then update:

```java
a = b;
b = temp;
```

Continue until:

```text
b = 0
```

Then:

```text
a = GCD
```

### Example: `gcd(48, 18)`

```text
48 % 18 = 12

a = 18
b = 12
```

Next:

```text
18 % 12 = 6

a = 12
b = 6
```

Next:

```text
12 % 6 = 0

a = 6
b = 0
```

Therefore:

```text
GCD = 6
```

### Remember the Pattern

```java
int temp = a % b;
a = b;
b = temp;
```

---

# 7. LCM

**LCM = Least Common Multiple**

It finds the smallest positive number that is divisible by both numbers.

### Example

For `12` and `18`:

```text
12 → 12, 24, 36, 48...
18 → 18, 36, 54...

LCM = 36
```

### Formula

```text
LCM(a, b) = (a × b) / GCD(a, b)
```

### Safe Java Code

```java
static long lcm(int a, int b) {
    return (long) a / gcd(a, b) * b;
}
```

### Why `(long)`?

Because:

```java
a * b
```

can overflow an `int` when the numbers are large.

So instead of directly doing:

```java
(a * b) / gcd(a, b)
```

we use:

```java
(long) a / gcd(a, b) * b
```

This is safer because the multiplication happens using `long`.

### Important Relationship

```text
GCD × LCM = a × b
```

Therefore:

```text
LCM = (a × b) / GCD
```

### Remember

```java
static long lcm(int a, int b) {
    return (long) a / gcd(a, b) * b;
}
```

---

# ⭐ Quick Revision Table

| Problem | Main Logic |
|---|---|
| Count | `count++` |
| Sum | `sum += value` |
| Maximum | `max = Math.max(max, value)` |
| Frequency | `frequency[value]++` |
| Prime | `n % i == 0` |
| GCD | `a % b` repeatedly |
| LCM | `(a / gcd(a,b)) * b` |

---

# 🧠 Remember These Patterns

### COUNT

```java
count++;
```

### SUM

```java
sum += value;
```

### MAXIMUM

```java
max = Math.max(max, value);
```

### FREQUENCY

```java
frequency[value]++;
```

### PRIME

```java
for (int i = 2; i * i <= n; i++) {
    if (n % i == 0) {
        prime = false;
        break;
    }
}
```

### GCD

```java
while (b != 0) {
    int temp = a % b;
    a = b;
    b = temp;
}
```

### LCM

```java
(long) a / gcd(a, b) * b;
```

---

# 🎯 How to Identify the Pattern

| If the question asks... | Think of... |
|---|---|
| **How many?** | Count |
| **What is the total?** | Sum |
| **What is the largest?** | Maximum |
| **How many times does each occur?** | Frequency |
| **Is the number prime?** | Prime |
| **What is the greatest common divisor?** | GCD |
| **What is the least common multiple?** | LCM |

---

## 🚀 Key Takeaway

These are **core DSA building blocks**.

Many beginner and intermediate problems are combinations of these patterns.

When you see a new problem, first ask:

> **Which basic pattern is this problem using?**

Once you identify the pattern, the solution becomes much easier to build.
