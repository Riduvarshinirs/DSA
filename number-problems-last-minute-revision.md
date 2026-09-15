# Number Problems — Prime, GCD & LCM
## Last-Minute Revision Notes

---

## 9. PRIME NUMBER

### Definition
A **prime number** has exactly **2 factors**:

- `1`
- itself

Examples:
- `2, 3, 5, 7` → Prime
- `4, 6` → Not Prime

### Beginner Approach
Check divisibility from `2` to `n - 1`.

```java
boolean prime = true;

if (n < 2) {
    prime = false;
}

for (int i = 2; i < n; i++) {
    if (n % i == 0) {
        prime = false;
        break;
    }
}
```

### ⭐ Optimized Approach
Only check up to **√n**.

**Reason:** If `n` has a factor greater than `√n`, its paired factor must be smaller than `√n`.

```java
boolean prime = true;

if (n < 2) {
    prime = false;
}

for (int i = 2; i * i <= n; i++) {
    if (n % i == 0) {
        prime = false;
        break;
    }
}
```

### Recognition
When asked **"Is N prime?"**:

```text
Need to find a divisor
        ↓
Try possible divisors
        ↓
Only check up to √N
```

### Complexity
| Approach | Time | Space |
|---|---:|---:|
| Brute force | O(n) | O(1) |
| Optimized | O(√n) | O(1) |

🔥 **Key takeaway:** Prime check → `i * i <= n`

---

# 10. GCD

**GCD = Greatest Common Divisor**

Example:

```text
12 → 1, 2, 3, 4, 6, 12
18 → 1, 2, 3, 6, 9, 18

GCD(12, 18) = 6
```

## ⭐ Euclidean Algorithm

Main formula:

```text
gcd(a, b) = gcd(b, a % b)
```

Repeat until:

```text
b == 0
```

Then `a` is the GCD.

### Example

```text
gcd(18, 12)

18 % 12 = 6
gcd(12, 6)

12 % 6 = 0
gcd(6, 0)

Answer = 6
```

### Java

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

### Complexity
- **Time:** O(log(min(a, b)))
- **Space:** O(1)

🔥 **Remember:** GCD → Euclidean Algorithm

---

# 11. LCM

### Formula

```text
LCM(a, b) = |a × b| / GCD(a, b)
```

Example:

```text
a = 12
b = 18

GCD = 6

LCM = (12 × 18) / 6
    = 36
```

### Java

```java
static long lcm(int a, int b) {
    return (long) a / gcd(a, b) * b;
}
```

### ⚠️ Important Overflow Detail

Prefer:

```java
(long) a / gcd(a, b) * b
```

instead of:

```java
(long) (a * b)
```

Why?

`a * b` may overflow as an `int` **before** it gets converted to `long`.

🔥 **Safe pattern:**

```text
a / gcd(a,b) × b
```

with `long` conversion before multiplication.

---

# 🚀 QUICK MEMORY SHEET

### Prime
```java
for (int i = 2; i * i <= n; i++)
```

→ Check divisors only up to **√n**

### GCD
```java
while (b != 0) {
    int temp = a % b;
    a = b;
    b = temp;
}
return a;
```

→ **Euclidean Algorithm**

### LCM
```java
(long) a / gcd(a, b) * b
```

→ **LCM = product / GCD**

---

## 🧠 3 Things to Remember

1. **Prime → √n**
2. **GCD → Euclidean Algorithm**
3. **LCM → `(long) a / gcd(a,b) * b` to avoid overflow**
