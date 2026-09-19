# 🔥 DAY 2 — NUMBER PROBLEMS + FUNDAMENTAL PATTERNS

> **Goal:** Learn how to solve common integer/number problems using arithmetic, digit extraction, loops, conditions, and basic optimization.
>
> **Priority:** 🔥 MUST KNOW  
> **Estimated Study Time:** 3–4 hours  
> **Recommended split:** 70% problem solving → 20% concepts → 10% revision

---

# 🎯 Today's Goal

By the end of Day 2, you should be able to:

- Extract digits from an integer.
- Understand `% 10` and `/ 10`.
- Count the digits of a number.
- Find the sum of digits.
- Find the product of digits.
- Reverse an integer.
- Check whether a number is a palindrome.
- Check whether a number is positive, negative, even, or odd.
- Check divisibility using modulo.
- Find factors/divisors of a number.
- Check whether a number is prime.
- Count prime/factor-related properties.
- Understand GCD and LCM at a basic level.
- Recognize when brute force can be reduced by checking only up to `sqrt(n)`.
- Handle zero, negative numbers, overflow, and boundary cases.
- Translate a number problem into a clean Java solution.
- Explain the time and space complexity of your solution.

---

# 📌 Prerequisites

You should understand:

- Java variables and primitive data types.
- `if/else`.
- `for` and `while` loops.
- Arithmetic operators.
- `%` modulo.
- Basic methods.
- Basic `O(1)`, `O(n)`, and `O(n²)` complexity.

If Day 1 is not comfortable yet, revise it before continuing.

---

# 🔥 Priority

## 🔥 MUST KNOW

Day 2 number techniques are foundational because they teach a very important DSA skill:

> **Break a problem into small operations that you can repeat systematically.**

These techniques appear in:

- Placement coding assessments.
- Beginner LeetCode problems.
- HackerRank problems.
- Mathematical programming problems.
- Interview warm-up questions.
- Later patterns such as hashing, recursion, binary search, and number theory.

---

# 1. 🧑‍🎓 BEGINNER EXPLANATION — HOW A NUMBER IS MADE OF DIGITS

Consider:

```text
n = 4728
```

The digits are:

```text
4 7 2 8
```

From the right:

```text
ones       = 8
tens       = 2
hundreds   = 7
thousands  = 4
```

The most useful operations for extracting digits are:

```java
n % 10
```

and

```java
n / 10
```

when `n` is an integer.

---

# 2. THE TWO MOST IMPORTANT NUMBER OPERATIONS

## `% 10` → Get the last digit

```java
int digit = n % 10;
```

Example:

```text
n = 4728

4728 % 10 = 8
```

So:

```text
last digit = 8
```

---

## `/ 10` → Remove the last digit

```java
n = n / 10;
```

For integer `n`:

```text
4728 / 10 = 472
```

The decimal part is discarded.

---

## Together

This pattern is extremely important:

```java
int digit = n % 10;
n = n / 10;
```

It means:

```text
Take last digit
      ↓
Remove last digit
      ↓
Repeat
```

---

# 3. VISUALIZATION — DIGIT EXTRACTION

For:

```text
n = 4728
```

First:

```text
4728 % 10 = 8
4728 / 10 = 472
```

Then:

```text
472 % 10 = 2
472 / 10 = 47
```

Then:

```text
47 % 10 = 7
47 / 10 = 4
```

Then:

```text
4 % 10 = 4
4 / 10 = 0
```

Finally:

```text
n = 0
```

So the extracted digits are:

```text
8 → 2 → 7 → 4
```

Notice:

> Digit extraction from the right naturally gives the number in reverse order.

---

# 4. IMPORTANT TERMS

| Term | Meaning |
|---|---|
| Digit | One symbol from `0` to `9` |
| `%` / Modulo | Gives the remainder |
| Quotient | Result of integer division |
| Divisor | Number that divides another number |
| Factor | A number that divides another number exactly |
| Prime | Number greater than 1 with exactly two positive factors |
| Composite | Number greater than 1 with more than two positive factors |
| GCD | Greatest Common Divisor |
| LCM | Least Common Multiple |
| Palindrome | Reads the same forward and backward |
| Overflow | Value exceeds the storage range of a data type |

---

# 5. 🧑‍🎓 BEGINNER EXPLANATION — COUNT DIGITS

## Problem

Count how many digits are in an integer.

Example:

```text
n = 4728
```

Answer:

```text
4
```

---

## Key idea

Every time we do:

```java
n /= 10;
```

one digit disappears.

Therefore, count how many times we can divide by `10` before reaching `0`.

---

## Algorithm

```text
count = 0

while n > 0:
    remove one digit
    count++

return count
```

---

## Java

```java
class Solution {

    public int countDigits(int n) {

        int count = 0;

        while (n > 0) {
            n = n / 10;
            count++;
        }

        return count;
    }
}
```

---

## Dry Run

Input:

```text
4728
```

| Step | `n` before | `n / 10` | Count |
|---:|---:|---:|---:|
| 1 | 4728 | 472 | 1 |
| 2 | 472 | 47 | 2 |
| 3 | 47 | 4 | 3 |
| 4 | 4 | 0 | 4 |

Answer:

```text
4
```

---

## ⚠️ Important Edge Case — `0`

The loop:

```java
while (n > 0)
```

does not execute for `0`.

But:

```text
0
```

contains one digit.

So a robust implementation should handle it:

```java
if (n == 0) {
    return 1;
}
```

---

## Negative Numbers

If the problem allows negative numbers, usually count digits of the absolute value.

```java
n = Math.abs(n);
```

But be careful with `Integer.MIN_VALUE`, because its absolute value cannot be represented as an `int`.

For general coding problems, use the constraints given by the problem.

---

## Complexity

If `d` is the number of digits:

```text
Time: O(d)
Space: O(1)
```

Since the number of decimal digits is approximately `log10(n)`, this can also be described as:

```text
Time: O(log n)
Space: O(1)
```

---

# 6. 🧠 HOW TO RECOGNIZE DIGIT-COUNTING

Think about digit extraction when the problem asks:

- Number of digits.
- Process every digit.
- Count odd/even digits.
- Sum digits.
- Product of digits.
- Reverse a number.
- Check a digit property.

### Keywords / Clues

- "digits of a number"
- "each digit"
- "last digit"
- "reverse"
- "sum of digits"
- "number of digits"

### Ask Yourself

1. Can I repeatedly use `% 10`?
2. Can I repeatedly divide by `10`?
3. What should happen to each extracted digit?
4. When should the loop stop?

---

# 7. 🧑‍🎓 BEGINNER EXPLANATION — SUM OF DIGITS

Example:

```text
4728
```

Sum:

```text
4 + 7 + 2 + 8 = 21
```

---

## Approach

Extract each digit:

```text
8
2
7
4
```

and add it to a running sum.

---

## Java

```java
class Solution {

    public int sumDigits(int n) {

        n = Math.abs(n);

        int sum = 0;

        while (n > 0) {

            int digit = n % 10;

            sum += digit;

            n /= 10;
        }

        return sum;
    }
}
```

---

## Dry Run

For:

```text
n = 4728
```

```text
sum = 0

digit = 8
sum = 8
n = 472

digit = 2
sum = 10
n = 47

digit = 7
sum = 17
n = 4

digit = 4
sum = 21
n = 0
```

Answer:

```text
21
```

---

## Complexity

```text
Time: O(log n)
Space: O(1)
```

The loop executes once per digit.

---

# 8. 🧑‍🎓 BEGINNER EXPLANATION — PRODUCT OF DIGITS

For:

```text
234
```

Product:

```text
2 × 3 × 4 = 24
```

Initialize:

```java
product = 1;
```

not `0`, because multiplying by zero would make every result zero.

---

## Java

```java
class Solution {

    public int productDigits(int n) {

        n = Math.abs(n);

        if (n == 0) {
            return 0;
        }

        int product = 1;

        while (n > 0) {

            int digit = n % 10;

            product *= digit;

            n /= 10;
        }

        return product;
    }
}
```

---

## ⚠️ Edge Cases

- `n = 0` → product is `0`.
- A number containing a zero digit → product becomes `0`.
- Very large products may overflow `int`; check constraints.

---

# 9. 🧑‍🎓 BEGINNER EXPLANATION — REVERSE AN INTEGER

Given:

```text
1234
```

return:

```text
4321
```

---

## Key idea

Extract digits from right to left.

```text
1234 → 4
123  → 3
12   → 2
1    → 1
```

But how do we build:

```text
4321
```

?

Use:

```java
reverse = reverse * 10 + digit;
```

---

# 10. WHY `reverse * 10 + digit` WORKS

Suppose:

```text
reverse = 43
digit = 2
```

We want:

```text
432
```

Do:

```text
43 × 10 + 2
= 430 + 2
= 432
```

Therefore:

```java
reverse = reverse * 10 + digit;
```

is the standard digit-reversal pattern.

---

# 11. JAVA — REVERSE INTEGER

```java
class Solution {

    public int reverse(int x) {

        int reverse = 0;

        while (x != 0) {

            int digit = x % 10;

            reverse = reverse * 10 + digit;

            x /= 10;
        }

        return reverse;
    }
}
```

For basic positive values, this works directly.

However, real coding platforms may include negative numbers and overflow.

---

# 12. ROBUST INTEGER REVERSAL

For a problem where the answer must fit in a 32-bit signed integer:

```java
class Solution {

    public int reverse(int x) {

        long reverse = 0;

        while (x != 0) {

            int digit = x % 10;

            reverse = reverse * 10 + digit;

            x /= 10;
        }

        if (reverse > Integer.MAX_VALUE ||
            reverse < Integer.MIN_VALUE) {
            return 0;
        }

        return (int) reverse;
    }
}
```

Using `long` for the intermediate result prevents the reversal calculation itself from overflowing before the final range check.

---

# 13. DRY RUN — REVERSE INTEGER

Input:

```text
1234
```

Start:

```text
reverse = 0
```

### Step 1

```text
digit = 4
reverse = 0 × 10 + 4
        = 4
x = 123
```

### Step 2

```text
digit = 3
reverse = 4 × 10 + 3
        = 43
x = 12
```

### Step 3

```text
digit = 2
reverse = 43 × 10 + 2
        = 432
x = 1
```

### Step 4

```text
digit = 1
reverse = 432 × 10 + 1
        = 4321
x = 0
```

Answer:

```text
4321
```

---

# 14. 🐌 BRUTE FORCE → 🚀 OPTIMAL: REVERSE

## 🐌 Brute Force

A straightforward approach is:

```text
Convert number → String
Reverse String → Convert back to number
```

For example:

```text
1234
↓
"1234"
↓
"4321"
↓
4321
```

This can be easy to understand, but it may be disallowed by problems that explicitly ask for arithmetic reversal.

---

## 🔍 Why learn the arithmetic approach?

Because:

- It teaches digit extraction.
- It avoids unnecessary string conversion.
- It directly models the number.
- It is a reusable pattern for many number problems.

---

## 🚀 Optimal / Arithmetic Approach

```text
last digit = n % 10
remove digit = n / 10
append digit = reverse * 10 + digit
```

---

## Complexity

If `d` is the number of digits:

```text
Time: O(d) = O(log n)
Space: O(1)
```

---

# 15. ⚠️ REVERSE INTEGER EDGE CASES

Consider:

### Case 1 — Single digit

```text
7 → 7
```

### Case 2 — Trailing zero

```text
1200 → 21
```

Leading zeroes in the reversed integer are not retained.

### Case 3 — Negative

```text
-123 → -321
```

### Case 4 — Overflow

A reversal may exceed the `int` range.

The exact problem constraints determine the required handling.

---

# 16. 🧑‍🎓 BEGINNER EXPLANATION — PALINDROME NUMBER

A palindrome reads the same forward and backward.

Examples:

```text
121 → palindrome
1221 → palindrome
7 → palindrome
123 → not palindrome
```

Visualization:

```text
121
↑ ↑
1 = 1

1221
↑  ↑
1  = 1
  ↑
  2 = 2
```

---

# 17. PALINDROME — BASIC APPROACH

Keep the original number.

Reverse a copy.

Compare:

```text
original == reversed
```

---

## Java

```java
class Solution {

    public boolean isPalindrome(int x) {

        if (x < 0) {
            return false;
        }

        int original = x;
        int reverse = 0;

        while (x != 0) {

            int digit = x % 10;

            reverse = reverse * 10 + digit;

            x /= 10;
        }

        return original == reverse;
    }
}
```

---

## Dry Run

Input:

```text
121
```

```text
original = 121

digit = 1
reverse = 1

digit = 2
reverse = 12

digit = 1
reverse = 121
```

Compare:

```text
121 == 121
```

Answer:

```text
true
```

---

# 18. PALINDROME — NEGATIVE NUMBERS

For the standard integer palindrome problem:

```text
-121
```

is not a palindrome.

Why?

Forward:

```text
-121
```

Backward:

```text
121-
```

They are not the same.

The official LeetCode problem also explicitly treats negative integers as non-palindromes. citeturn0search2

---

# 19. PALINDROME — TRAILING ZERO

Consider:

```text
10
```

Reverse:

```text
01
```

As an integer, that becomes:

```text
1
```

Therefore:

```text
10 != 1
```

So `10` is not a palindrome.

---

# 20. 🚀 PALINDROME OPTIMIZATION IDEA

For advanced versions, you do not necessarily need to reverse the entire number.

You can reverse only half and compare the two halves.

This avoids some overflow concerns and can reduce the amount of work.

The important idea is:

```text
left half
    ↕
right half reversed
```

You do not need to memorize the optimized half-reversal implementation today.

First master the full reversal method.

---

# 21. 🧠 HOW TO RECOGNIZE PALINDROME PROBLEMS

Think palindrome when you see:

- "reads the same forward and backward"
- "same from both directions"
- "reverse equals original"
- "symmetric"

### Ask Yourself

1. Can I compare the original with its reverse?
2. Can I compare corresponding left/right digits?
3. Are negative values allowed?
4. Are leading/trailing zeroes relevant?

---

# 22. 🧑‍🎓 BEGINNER EXPLANATION — ARMSTRONG / NARCISSISTIC NUMBERS

A common number problem is checking whether a number equals the sum of its digits raised to the number of digits.

For a 3-digit number:

```text
153
```

we calculate:

```text
1³ + 5³ + 3³
= 1 + 125 + 27
= 153
```

Therefore `153` is an Armstrong number.

For modern coding interviews, this is mainly a practice problem for:

- Digit extraction.
- Loops.
- Powers.
- Counting digits.
- Careful implementation.

It is not as universally important as arrays, hashing, binary search, or sliding window.

**Priority:** 🟡 GOOD TO KNOW

---

## Java — 3-digit version

```java
class Solution {

    public boolean isArmstrong(int n) {

        int original = n;
        int sum = 0;

        while (n > 0) {

            int digit = n % 10;

            sum += digit * digit * digit;

            n /= 10;
        }

        return sum == original;
    }
}
```

This version specifically handles the 3-digit definition.

For a generalized `k`-digit Armstrong number, calculate the digit count first and raise every digit to `k`.

---

# 23. 🧑‍🎓 BEGINNER EXPLANATION — FACTORS / DIVISORS

A factor of `n` is a number that divides `n` exactly.

For:

```text
12
```

factors are:

```text
1, 2, 3, 4, 6, 12
```

because:

```text
12 % 1 = 0
12 % 2 = 0
12 % 3 = 0
12 % 4 = 0
12 % 6 = 0
12 % 12 = 0
```

---

# 24. BRUTE FORCE FACTOR SEARCH

The simplest method:

```java
for (int i = 1; i <= n; i++) {

    if (n % i == 0) {
        System.out.println(i);
    }
}
```

---

## Complexity

```text
Time: O(n)
Space: O(1)
```

This is correct but can be improved.

---

# 25. 🔍 KEY OBSERVATION — FACTOR PAIRS

Factors occur in pairs.

For:

```text
36
```

we have:

```text
1 × 36
2 × 18
3 × 12
4 × 9
6 × 6
```

After `6`, the pairs repeat in reverse.

And:

```text
sqrt(36) = 6
```

Therefore, we only need to check up to:

```text
sqrt(n)
```

---

# 26. 🚀 OPTIMAL FACTOR ENUMERATION

```java
class Solution {

    public void printFactors(int n) {

        for (int i = 1; i * i <= n; i++) {

            if (n % i == 0) {

                System.out.print(i + " ");

                if (i != n / i) {
                    System.out.print(n / i + " ");
                }
            }
        }
    }
}
```

For sorted output, collect the small and large factors separately or sort the result afterward.

---

## Why `i != n / i`?

For:

```text
36
```

when:

```text
i = 6
```

we get:

```text
n / i = 6
```

We should print `6` only once.

---

# 27. COMPLEXITY — FACTORS

Brute force:

```text
Time: O(n)
Space: O(1)
```

Square-root approach:

```text
Time: O(sqrt(n))
Space: O(1)
```

Why?

The loop checks:

```text
1, 2, 3, ..., sqrt(n)
```

instead of:

```text
1, 2, 3, ..., n
```

---

# 28. 🧠 PATTERN RECOGNITION — SQRT OPTIMIZATION

Think about checking up to `sqrt(n)` when:

- Finding factors.
- Checking primality.
- Enumerating divisor pairs.

### Keywords / Clues

- "divisor"
- "factor"
- "prime"
- "divides exactly"
- "factor pairs"

### Ask Yourself

1. Do factors come in pairs?
2. Does checking beyond `sqrt(n)` repeat information?
3. Can I check `i * i <= n`?

---

# 29. 🧑‍🎓 BEGINNER EXPLANATION — PRIME NUMBERS

A prime number is a number greater than `1` with exactly two positive factors:

```text
1 and itself
```

Examples:

```text
2
3
5
7
11
13
```

Not prime:

```text
1
4
6
8
9
10
```

---

# 30. IMPORTANT PRIME EDGE CASES

### `1`

```text
1 is NOT prime.
```

It has only one positive factor.

### `0`

```text
0 is NOT prime.
```

### Negative numbers

Negative integers are not prime under the standard positive-integer definition.

---

# 31. 🐌 BRUTE FORCE PRIME CHECK

Try every number from:

```text
2 to n - 1
```

If anything divides `n`, it is not prime.

```java
class Solution {

    public boolean isPrime(int n) {

        if (n < 2) {
            return false;
        }

        for (int i = 2; i < n; i++) {

            if (n % i == 0) {
                return false;
            }
        }

        return true;
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

# 32. 🚀 OPTIMAL PRIME CHECK — SQRT

If `n` is composite, it must have a factor less than or equal to `sqrt(n)`.

Therefore:

```java
class Solution {

    public boolean isPrime(int n) {

        if (n < 2) {
            return false;
        }

        for (int i = 2; i * i <= n; i++) {

            if (n % i == 0) {
                return false;
            }
        }

        return true;
    }
}
```

---

# 33. DRY RUN — PRIME CHECK

Input:

```text
n = 29
```

Check:

```text
i = 2
29 % 2 != 0

i = 3
29 % 3 != 0

i = 4
29 % 4 != 0

i = 5
29 % 5 != 0
```

Now:

```text
6 × 6 > 29
```

Stop.

No divisor found.

Therefore:

```text
29 is prime
```

---

# 34. PRIME COMPLEXITY

```text
Time: O(sqrt(n))
Space: O(1)
```

This is much better than `O(n)` for large numbers.

---

# 35. ⚠️ INTEGER OVERFLOW IN `i * i`

This condition:

```java
i * i <= n
```

can overflow if `i` becomes very large.

A safer version is:

```java
i <= n / i
```

For typical beginner constraints, `i * i <= n` is easy to understand.

For robust code with large integers:

```java
for (int i = 2; i <= n / i; i++) {
    ...
}
```

---

# 36. 🧠 HOW TO RECOGNIZE PRIME PROBLEMS

Think about prime checking when you see:

- "Is `n` prime?"
- "Count primes."
- "Find prime factors."
- "Number has exactly two divisors."

First question:

> Can I eliminate candidates up to `sqrt(n)`?

---

# 37. 🧑‍🎓 BEGINNER EXPLANATION — GCD

GCD means:

> **Greatest Common Divisor**

For:

```text
12 and 18
```

common divisors:

```text
1, 2, 3, 6
```

Greatest:

```text
6
```

Therefore:

```text
GCD(12, 18) = 6
```

---

# 38. EUCLIDEAN ALGORITHM

The key identity is:

```text
gcd(a, b) = gcd(b, a % b)
```

Repeat until:

```text
b = 0
```

Then:

```text
a
```

is the GCD.

---

# 39. DRY RUN — GCD

Find:

```text
gcd(48, 18)
```

Step 1:

```text
48 % 18 = 12
```

Now:

```text
gcd(18, 12)
```

Step 2:

```text
18 % 12 = 6
```

Now:

```text
gcd(12, 6)
```

Step 3:

```text
12 % 6 = 0
```

Now:

```text
gcd(6, 0)
```

Answer:

```text
6
```

---

# 40. JAVA — GCD

```java
class Solution {

    public int gcd(int a, int b) {

        a = Math.abs(a);
        b = Math.abs(b);

        while (b != 0) {

            int remainder = a % b;

            a = b;
            b = remainder;
        }

        return a;
    }
}
```

---

## Complexity

```text
Time: O(log(min(a, b)))
Space: O(1)
```

The Euclidean algorithm reduces the numbers rapidly.

---

# 41. 🧑‍🎓 BEGINNER EXPLANATION — LCM

LCM means:

> **Least Common Multiple**

For:

```text
4 and 6
```

multiples:

```text
4:  4, 8, 12, 16, ...
6:  6, 12, 18, ...
```

Smallest common positive multiple:

```text
12
```

Therefore:

```text
LCM(4, 6) = 12
```

---

# 42. GCD–LCM RELATIONSHIP

For positive integers:

```text
gcd(a,b) × lcm(a,b) = a × b
```

Therefore:

```text
lcm(a,b) = (a / gcd(a,b)) × b
```

Prefer this form:

```java
(a / gcd(a, b)) * b
```

instead of:

```java
(a * b) / gcd(a, b)
```

because multiplying first may overflow earlier.

---

# 43. JAVA — LCM

```java
class Solution {

    public long lcm(int a, int b) {

        long x = Math.abs((long) a);
        long y = Math.abs((long) b);

        if (x == 0 || y == 0) {
            return 0;
        }

        long gcd = gcd(x, y);

        return (x / gcd) * y;
    }

    private long gcd(long a, long b) {

        while (b != 0) {

            long temp = a % b;

            a = b;
            b = temp;
        }

        return a;
    }
}
```

---

# 44. 🧠 PATTERN RECOGNITION — GCD / LCM

Think GCD when you see:

- Greatest common divisor.
- Largest number dividing both.
- Simplifying ratios.
- Repeated divisibility.

Think LCM when you see:

- Smallest common multiple.
- Events repeating at different intervals.
- "When will both cycles meet again?"

---

# 45. EXAMPLE — COUNT DIGITS THAT DIVIDE A NUMBER

Given:

```text
n = 12
```

Digits:

```text
1, 2
```

Check:

```text
12 % 1 = 0
12 % 2 = 0
```

Answer:

```text
2
```

For:

```text
n = 1012
```

digit `0` must be skipped because division by zero is undefined.

The HackerRank **Find Digits** problem uses exactly this idea. citeturn0search0

---

## Java

```java
class Solution {

    public int countDividingDigits(int n) {

        int original = n;
        int count = 0;

        while (n > 0) {

            int digit = n % 10;

            if (digit != 0 && original % digit == 0) {
                count++;
            }

            n /= 10;
        }

        return count;
    }
}
```

---

## Complexity

```text
Time: O(log n)
Space: O(1)
```

---

# 46. EXAMPLE — NUMBER OF STEPS TO REDUCE A NUMBER TO ZERO

Suppose:

```text
n = 14
```

Rules:

```text
If n is even:
    divide by 2

Otherwise:
    subtract 1
```

Dry run:

```text
14 → 7 → 6 → 3 → 2 → 1 → 0
```

Number of steps:

```text
6
```

This is a good beginner problem because it combines:

- Conditionals.
- Modulo.
- Loops.
- Simulation.

---

## Java

```java
class Solution {

    public int numberOfSteps(int num) {

        int steps = 0;

        while (num > 0) {

            if (num % 2 == 0) {
                num /= 2;
            } else {
                num--;
            }

            steps++;
        }

        return steps;
    }
}
```

---

## Complexity

Each operation reduces the number substantially or decreases it by one.

For this problem, the number of operations is bounded logarithmically for the repeated halving portions, with at most a linear number of subtractions between them; the standard accepted bound is:

```text
Time: O(log n)
Space: O(1)
```

---

# 47. EXAMPLE — BEAUTIFUL DAYS

HackerRank's **Beautiful Days at the Movies** asks you to reverse each day number, calculate the absolute difference between the day and its reverse, and check whether that difference is divisible by `k`. citeturn0search1

Example:

```text
20 23 6
```

Check each day:

```text
20 → reverse 02 → 2
|20 - 2| = 18
18 % 6 = 0 → beautiful

21 → 12
|21 - 12| = 9
9 % 6 != 0

22 → 22
|22 - 22| = 0
0 % 6 = 0 → beautiful

23 → 32
|23 - 32| = 9
9 % 6 != 0
```

Answer:

```text
2
```

---

# 48. 🧠 THIS IS A PATTERN, NOT A SINGLE PROBLEM

Notice what happened:

```text
Range
 ↓
For every number
 ↓
Reverse number
 ↓
Calculate difference
 ↓
Check divisibility
 ↓
Count
```

This is **simulation built from smaller patterns**.

That is an important DSA skill:

> A harder-looking problem can often be decomposed into several simple patterns.

---

# 49. 🧠 NUMBER-PROBLEM PATTERN MAP

```text
Number Problem
      |
      +---- Need last digit?
      |       ↓
      |      n % 10
      |
      +---- Need to remove last digit?
      |       ↓
      |      n / 10
      |
      +---- Need reverse?
      |       ↓
      |      rev = rev * 10 + digit
      |
      +---- Need every digit?
      |       ↓
      |      while (n > 0)
      |
      +---- Need factors?
      |       ↓
      |      i * i <= n
      |
      +---- Need prime?
      |       ↓
      |      check divisors up to sqrt(n)
      |
      +---- Need GCD?
      |       ↓
      |      Euclidean algorithm
```

---

# 50. 🧠 BRUTE FORCE → OPTIMAL THINKING

Day 2 introduces an important optimization pattern.

## Example: Prime Check

### Brute force

```text
Try every number:
2, 3, 4, ..., n-1
```

Complexity:

```text
O(n)
```

### Key observation

Factors come in pairs.

If:

```text
n = a × b
```

and both `a` and `b` were greater than `sqrt(n)`, then:

```text
a × b > n
```

which is impossible.

Therefore at least one factor is:

```text
<= sqrt(n)
```

### Optimization

```text
Check only up to sqrt(n)
```

Complexity:

```text
O(sqrt(n))
```

---

# 51. EDGE CASE MASTER LIST

For number problems, actively check:

### Zero

```text
0
```

Questions:

- How many digits?
- Is it prime?
- What is its digit sum?
- What happens during division?

### One

```text
1
```

Remember:

```text
1 is not prime.
```

### Negative

```text
-123
```

Ask whether the problem allows negative values.

### Trailing zero

```text
1200
```

Reverse becomes:

```text
21
```

### Repeated digits

```text
1111
```

Useful for testing palindrome/counting logic.

### Large values

Check whether:

```text
int
```

is sufficient or:

```text
long
```

is required.

---

# 52. ❌ COMMON BEGINNER MISTAKES

## Mistake 1 — Forgetting `% 10`

Wrong approach:

```java
digit = n / 10;
```

That removes the last digit.

Correct:

```java
digit = n % 10;
```

---

## Mistake 2 — Forgetting to reduce `n`

Wrong:

```java
while (n > 0) {
    int digit = n % 10;
}
```

`n` never changes.

This creates an infinite loop.

Correct:

```java
n /= 10;
```

---

## Mistake 3 — Starting product at zero

Wrong:

```java
int product = 0;
```

Then every multiplication remains zero.

Correct:

```java
int product = 1;
```

with a separate `n == 0` case if required.

---

## Mistake 4 — Treating `1` as prime

```text
1 is not prime.
```

---

## Mistake 5 — Dividing by zero

Never do:

```java
n % digit
```

without checking:

```java
digit != 0
```

if `digit` can be zero.

---

## Mistake 6 — Ignoring overflow during reversal

This can be unsafe:

```java
int reverse = reverse * 10 + digit;
```

for unconstrained integer reversal.

Use a `long` intermediate when the problem requires overflow protection.

---

## Mistake 7 — Checking factors all the way to `n`

Correct but often unnecessarily slow:

```java
for (int i = 1; i <= n; i++)
```

For factor/primality checks, consider:

```java
i * i <= n
```

or:

```java
i <= n / i
```

---

## Mistake 8 — Changing the original number and then trying to use it

If you need the original value later:

```java
int original = n;
```

before modifying `n`.

---

# 53. JAVA-SPECIFIC NOTES

## `Math.abs()`

Useful:

```java
n = Math.abs(n);
```

But remember that `Math.abs(Integer.MIN_VALUE)` remains negative because that value has no positive representation in `int`.

Use `long` if constraints require handling that case safely.

---

## `Math.pow()`

`Math.pow()` returns a `double`.

For simple integer-power problems, direct multiplication is often clearer:

```java
digit * digit * digit
```

rather than:

```java
(int) Math.pow(digit, 3)
```

---

## Integer division

```java
17 / 10
```

returns:

```text
1
```

This is exactly why:

```java
n /= 10;
```

removes the last digit.

---

## `long`

Use:

```java
long value = 10000000000L;
```

when the range requires values larger than `int`.

---

# 54. 🧪 TRY YOURSELF — MINI PRACTICE

Do not open the solutions immediately.

## Problem 1

Given an integer `n`, return the sum of its digits.

Example:

```text
Input: 583
Output: 16
```

<details>
<summary>💡 Hint</summary>

Repeatedly:

```java
digit = n % 10;
n /= 10;
```

Maintain a `sum`.

</details>

<details>
<summary>✅ Solution</summary>

### Approach

Extract one digit at a time and add it to `sum`.

```java
class Solution {

    public int sumDigits(int n) {

        n = Math.abs(n);

        int sum = 0;

        while (n > 0) {
            sum += n % 10;
            n /= 10;
        }

        return sum;
    }
}
```

### Dry Run

```text
583

8 → sum = 8
3 → sum = 11
5 → sum = 16
```

### Complexity

```text
Time: O(log n)
Space: O(1)
```

### Edge Cases

- `n = 0`
- Negative input if permitted

</details>

---

## Problem 2

Given an integer `n`, return its reverse.

Example:

```text
Input: 5080
Output: 805
```

<details>
<summary>💡 Hint</summary>

Use:

```java
reverse = reverse * 10 + digit;
```

</details>

<details>
<summary>✅ Solution</summary>

```java
class Solution {

    public int reverse(int n) {

        int reverse = 0;

        while (n != 0) {

            int digit = n % 10;

            reverse = reverse * 10 + digit;

            n /= 10;
        }

        return reverse;
    }
}
```

For a platform problem with possible integer overflow, use a `long` intermediate and apply the required overflow rule.

### Complexity

```text
Time: O(log n)
Space: O(1)
```

</details>

---

# 55. 🧪 MINI PRACTICE — PRIME

## Problem 1

Check whether `37` is prime.

<details>
<summary>💡 Hint</summary>

You only need to test possible divisors up to:

```text
sqrt(37)
```

</details>

<details>
<summary>✅ Solution</summary>

```text
sqrt(37) ≈ 6.08
```

Check:

```text
2 → no
3 → no
4 → no
5 → no
6 → no
```

Therefore:

```text
37 is prime.
```

Complexity:

```text
O(sqrt(n))
```

</details>

---

## Problem 2

Check whether `49` is prime.

<details>
<summary>💡 Hint</summary>

Try `7`.

</details>

<details>
<summary>✅ Solution</summary>

```text
49 % 7 = 0
```

Therefore:

```text
49 is not prime.
```

</details>

---

# 56. 🧪 MINI PRACTICE — GCD

## Problem 1

Find:

```text
GCD(48, 18)
```

<details>
<summary>💡 Hint</summary>

Use:

```text
gcd(a,b) = gcd(b,a%b)
```

</details>

<details>
<summary>✅ Solution</summary>

```text
48 % 18 = 12
18 % 12 = 6
12 % 6 = 0

GCD = 6
```

</details>

---

## Problem 2

Find:

```text
GCD(20, 8)
```

<details>
<summary>💡 Hint</summary>

Keep replacing the pair with:

```text
(b, a % b)
```

</details>

<details>
<summary>✅ Solution</summary>

```text
20 % 8 = 4
8 % 4 = 0

GCD = 4
```

</details>

---

# 57. PRACTICE PROBLEMS

## 🟢 Easy

### 1. Palindrome Number

**Platform:** LeetCode  
**Difficulty:** Easy  
**Pattern:** Digit extraction / reverse  
**Why this pattern:** Compare a number with its reverse.  
**What you should notice:** Negative numbers are not palindromes in the standard problem.  
**Expected Complexity:** `O(log n)` time, `O(1)` extra space

https://leetcode.com/problems/palindrome-number/

The official problem is LeetCode 9, **Palindrome Number**, and includes the follow-up of solving it without converting the integer to a string. citeturn0search2

---

### 2. Find Digits

**Platform:** HackerRank  
**Difficulty:** Easy  
**Pattern:** Digit extraction + modulo  
**Why this pattern:** Extract each digit and test whether it divides the original number.  
**What you should notice:** Zero digits must be skipped before using `% digit`.  
**Expected Complexity:** `O(log n)` per number

https://www.hackerrank.com/challenges/find-digits/problem

HackerRank describes the task as counting digits that are divisors of the given integer. citeturn0search0

---

### 3. Beautiful Days at the Movies

**Platform:** HackerRank  
**Difficulty:** Easy  
**Pattern:** Reverse + simulation + divisibility  
**Why this pattern:** Combines several Day 2 techniques.  
**What you should notice:** For every value in a range, reverse it and test the difference.  
**Expected Complexity:** `O((j-i+1) × log j)`

https://www.hackerrank.com/challenges/beautiful-days-at-the-movies/problem

The official HackerRank statement defines a beautiful day using the difference between a day and its reverse divided by `k`. citeturn0search1

---

### 4. Number of Steps to Reduce a Number to Zero

**Platform:** LeetCode  
**Difficulty:** Easy  
**Pattern:** Simulation + modulo + loop  
**Why this pattern:** Reinforces condition-driven number processing.  
**What you should notice:** Even → divide; odd → subtract.  
**Expected Complexity:** Approximately `O(log n)` time for the standard problem, `O(1)` space

https://leetcode.com/problems/number-of-steps-to-reduce-a-number-to-zero/

---

## 🟡 Medium / Challenge

### 5. Reverse Integer

**Platform:** LeetCode  
**Difficulty:** Medium  
**Pattern:** Digit extraction + overflow handling  
**Why this pattern:** Builds directly on arithmetic reversal while introducing integer-range safety.  
**What you should notice:** The reversed value may exceed the 32-bit signed integer range.  
**Expected Complexity:** `O(log n)` time, `O(1)` extra space

https://leetcode.com/problems/reverse-integer/

---

### 6. Count Primes

**Platform:** LeetCode  
**Difficulty:** Medium  
**Pattern:** Prime numbers / sieve  
**Why this pattern:** Introduces the next level after checking one number for primality.  
**What you should notice:** Checking every number independently can be too slow; later you will learn the Sieve of Eratosthenes.  
**Expected Complexity:** Aim for better than checking every candidate independently.

https://leetcode.com/problems/count-primes/

---

## 🔴 Hard / Challenge

No hard problem is required for Day 2.

The priority is mastering:

```text
Digit extraction
Reverse
Palindrome
Factors
Prime
GCD
LCM
```

before moving to more advanced number theory.

---

# 58. PRACTICE ORDER

Follow this order:

```text
Very Easy
   ↓
Digit Sum
   ↓
Digit Count
   ↓
Reverse Number
   ↓
Palindrome Number
   ↓
Find Digits
   ↓
Beautiful Days
   ↓
Reverse Integer
   ↓
Count Primes
```

Do not skip the custom mini-practice.

The purpose is to build the pattern independently before using LeetCode.

---

# 59. 🎤 HOW TO EXPLAIN NUMBER-DIGIT PROBLEMS IN AN INTERVIEW

A strong explanation:

> "I can process the number one digit at a time using modulo 10 to extract the last digit and integer division by 10 to remove it."

> "For each extracted digit, I perform the required operation."

> "Because each iteration removes one digit, the loop runs once per digit."

> "Therefore, if the number has `d` digits, the time complexity is O(d), which is O(log n), and the extra space is O(1)."

---

# 60. 🎤 HOW TO EXPLAIN PRIME OPTIMIZATION

> "The brute-force approach checks every possible divisor up to n, giving O(n) time."

> "The key observation is that factors occur in pairs. If n is composite, at least one factor must be less than or equal to sqrt(n)."

> "Therefore, I only check divisors up to sqrt(n), reducing the complexity to O(sqrt(n))."

---

# 61. 📊 CONSTRAINT → ALGORITHM

For Day 2:

| Constraint / Situation | Consider |
|---|---|
| One number, few digits | Direct digit loop |
| Need every digit | `% 10` + `/ 10` |
| Check factors of one number | Up to `sqrt(n)` |
| Check whether one number is prime | Trial division up to `sqrt(n)` |
| Need GCD | Euclidean algorithm |
| Need LCM | GCD + formula |
| Very many prime queries | Later: Sieve / advanced number theory |
| Extremely large integer represented as text | String-based digit processing may be needed |

These are guidelines, not absolute rules.

---

# 62. 🧠 PATTERN RECOGNITION TEST

Identify the pattern **before** solving.

### 1.

> Given `n`, calculate the sum of all its digits.

**Pattern:** Digit extraction.

---

### 2.

> Determine whether `121` reads the same backward.

**Pattern:** Reverse / palindrome.

---

### 3.

> Determine whether `97` is prime.

**Pattern:** Factor checking up to `sqrt(n)`.

---

### 4.

> Find all divisors of `60`.

**Pattern:** Factor enumeration / factor pairs.

---

### 5.

> Find the greatest number that divides both `24` and `36`.

**Pattern:** GCD.

---

### 6.

> Find the smallest positive number divisible by both `8` and `12`.

**Pattern:** LCM.

---

### 7.

> Count how many digits of `128` divide `128`.

**Pattern:** Digit extraction + divisibility.

---

### 8.

> Reverse every number between `20` and `50` and test a condition.

**Pattern:** Range simulation + digit reversal.

---

### 9.

> Count how many times you can remove the last digit before the number becomes zero.

**Pattern:** Digit count.

---

### 10.

> A number is transformed differently depending on whether it is even or odd.

**Pattern:** Modulo + simulation.

---

# 63. 📝 DAILY QUIZ — 10 QUESTIONS

## Q1 — MCQ

For:

```java
int n = 4728;
```

what is:

```java
n % 10
```

?

A. `472`  
B. `8`  
C. `2`  
D. `0`

---

## Q2 — MCQ

Which operation removes the last digit of a positive integer?

A. `n % 10`  
B. `n * 10`  
C. `n / 10`  
D. `n + 10`

---

## Q3 — Output Prediction

What is printed?

```java
int n = 1234;
int digit = n % 10;

System.out.println(digit);
```

A. `1`  
B. `2`  
C. `3`  
D. `4`

---

## Q4 — Complexity

What is the complexity of processing every digit of `n` using:

```java
while (n > 0) {
    n /= 10;
}
```

A. `O(1)`  
B. `O(n)`  
C. `O(log n)`  
D. `O(n²)`

---

## Q5 — Concept

Why is `1` not a prime number?

---

## Q6 — Debugging

What is the problem here?

```java
while (n > 0) {
    int digit = n % 10;
    System.out.println(digit);
}
```

---

## Q7 — Pattern Recognition

You need to determine whether `12321` is the same forward and backward.

Which pattern should you consider?

A. Binary Search  
B. Palindrome / reverse  
C. BFS  
D. HashMap

---

## Q8 — MCQ

What is the optimized complexity for checking whether one integer `n` is prime using trial division?

A. `O(1)`  
B. `O(log n)`  
C. `O(sqrt(n))`  
D. `O(n²)`

---

## Q9 — Small Coding

Write the key statement that appends an extracted digit to a reversed number.

---

## Q10 — GCD

Calculate:

```text
GCD(48, 18)
```

---

# 64. 📝 ANSWER KEY

### Q1

**B. `8`**

```text
4728 % 10 = 8
```

### Q2

**C. `n / 10`**

Integer division removes the last digit.

### Q3

**D. `4`**

The last digit is `4`.

### Q4

**C. `O(log n)`**

The number of decimal digits grows logarithmically with `n`.

### Q5

`1` has only one positive divisor, itself. A prime must have exactly two positive divisors.

### Q6

`n` is never changed.

Add:

```java
n /= 10;
```

Otherwise the loop can run forever.

### Q7

**B. Palindrome / reverse**

### Q8

**C. `O(sqrt(n))`**

### Q9

```java
reverse = reverse * 10 + digit;
```

### Q10

```text
48 % 18 = 12
18 % 12 = 6
12 % 6 = 0

GCD = 6
```

---

# 65. 🔁 QUICK REVISION

## Remember These

```text
Last digit:
n % 10

Remove last digit:
n / 10

Reverse:
reverse = reverse * 10 + digit

Digit processing:
while (n > 0)

Factor checking:
i * i <= n

Prime:
n < 2 → not prime

GCD:
gcd(a,b) = gcd(b, a%b)

LCM:
(a / gcd(a,b)) * b
```

---

## Important Templates

### Digit extraction

```java
while (n > 0) {

    int digit = n % 10;

    // process digit

    n /= 10;
}
```

### Sum of digits

```java
int sum = 0;

while (n > 0) {

    sum += n % 10;

    n /= 10;
}
```

### Reverse

```java
int reverse = 0;

while (n != 0) {

    int digit = n % 10;

    reverse = reverse * 10 + digit;

    n /= 10;
}
```

### Palindrome

```java
int original = n;
int reverse = 0;

while (n != 0) {

    int digit = n % 10;

    reverse = reverse * 10 + digit;

    n /= 10;
}

return original == reverse;
```

### Prime

```java
if (n < 2) {
    return false;
}

for (int i = 2; i <= n / i; i++) {

    if (n % i == 0) {
        return false;
    }
}

return true;
```

### GCD

```java
while (b != 0) {

    int remainder = a % b;

    a = b;
    b = remainder;
}

return a;
```

---

## Complexity Cheat Sheet

| Technique | Time | Extra Space |
|---|---:|---:|
| Digit processing | `O(log n)` | `O(1)` |
| Reverse integer | `O(log n)` | `O(1)` |
| Palindrome by reversal | `O(log n)` | `O(1)` |
| Factors by brute force | `O(n)` | `O(1)` |
| Factors using sqrt | `O(sqrt(n))` | `O(1)` |
| Prime by brute force | `O(n)` | `O(1)` |
| Prime using sqrt | `O(sqrt(n))` | `O(1)` |
| GCD — Euclidean algorithm | `O(log(min(a,b)))` | `O(1)` |
| LCM using GCD | `O(log(min(a,b)))` | `O(1)` |

---

## Recognition Cheat Sheet

| If you see... | Think... |
|---|---|
| Last digit | `% 10` |
| Remove last digit | `/ 10` |
| Every digit | `while (n > 0)` |
| Reverse number | `reverse * 10 + digit` |
| Same forward/backward | Palindrome |
| Divisor/factor | `%` |
| Factor pairs | `sqrt(n)` |
| Prime | Check up to `sqrt(n)` |
| Greatest common divisor | Euclidean algorithm |
| Least common multiple | GCD formula |
| Even/odd | `% 2` |
| Digit divides number | `original % digit == 0` |
| Range of numbers + repeated rule | Simulation |

---

# 66. 🏠 HOMEWORK

## Must Solve

1. LeetCode — **Palindrome Number**
2. HackerRank — **Find Digits**
3. HackerRank — **Beautiful Days at the Movies**
4. LeetCode — **Number of Steps to Reduce a Number to Zero**
5. Write your own `reverse(int n)` method.
6. Write your own `isPrime(int n)` method.
7. Write your own `gcd(int a, int b)` method.

## Optional Challenge

8. LeetCode — **Reverse Integer**
9. LeetCode — **Count Primes**
10. Implement factor enumeration in `O(sqrt(n))`.

---

# 67. DAY-END CHECKLIST

- [ ] I understand the basic concept
- [ ] I can explain `% 10`
- [ ] I can explain `/ 10`
- [ ] I can extract every digit of a number
- [ ] I can count digits
- [ ] I can calculate digit sum
- [ ] I can reverse an integer
- [ ] I can check a palindrome
- [ ] I understand factor pairs
- [ ] I can check whether a number is prime
- [ ] I understand why `sqrt(n)` is enough for trial division
- [ ] I can calculate GCD
- [ ] I can calculate LCM
- [ ] I know how to handle zero
- [ ] I know `1` is not prime
- [ ] I understand integer overflow concerns
- [ ] I solved the easy problems
- [ ] I attempted the challenge problems
- [ ] I completed the quiz
- [ ] I can explain the digit-processing pattern without notes

---

# 68. 🚦 READY FOR DAY 3?

Once these patterns are comfortable, move to:

➡️ [Day 3 — Arrays Fundamentals](Day-03-Arrays-Fundamentals.md)

⬅️ [Previous Day — Java Basics](Day-01-Java-Basics.md)  
➡️ [Next Day — Arrays Fundamentals](Day-03-Arrays-Fundamentals.md)

---

# 🎯 FINAL DAY 2 MINDSET

When you see a number problem, do not immediately search for a formula.

Start with:

```text
What exactly is being asked?
        ↓
Do I need each digit?
        ↓
Use % 10 and / 10
        ↓
What should I do with the digit?
        ↓
Sum / count / multiply / reverse / compare
        ↓
Can I avoid repeated work?
        ↓
Check constraints
        ↓
Handle edge cases
        ↓
Calculate complexity
```

The most important Day 2 pattern is:

```text
NUMBER
  ↓
Extract last digit
  ↓
Process digit
  ↓
Remove last digit
  ↓
Repeat
```

Master this.

It will make many "number problems" stop looking mysterious.

---

**End of Day 2**
