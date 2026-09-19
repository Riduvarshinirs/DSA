# 🔥 DAY 5 — STRINGS + HASHING

> **Goal:** Learn how to work with strings efficiently and use hashing to turn repeated searching/counting into fast lookups.
>
> **Priority:** 🔥🔥🔥 VERY HIGH  
> **Estimated Study Time:** 4–5 hours  
> **Recommended split:** 70% problem solving → 20% concepts → 10% revision

---

# 🎯 Today's Goal

By the end of today, you should be able to:

- Understand Java `String` fundamentals.
- Understand characters, indices, and string traversal.
- Use `charAt()`, `length()`, `substring()`, `equals()`, and `toCharArray()`.
- Understand why Java Strings are immutable.
- Compare strings correctly in Java.
- Build strings using `StringBuilder`.
- Understand ASCII-style character indexing for lowercase English letters.
- Understand the idea of hashing.
- Use frequency arrays for small fixed character sets.
- Use `HashMap` for general key-value counting.
- Use `HashSet` for uniqueness/existence checks.
- Count character frequencies.
- Find duplicate and unique characters.
- Check whether two strings are anagrams.
- Solve Two Sum using hashing.
- Understand the difference between `HashSet` and `HashMap`.
- Recognize when hashing is useful.
- Understand brute force → hashing optimization.
- Understand substring vs subsequence.
- Get an introduction to string + sliding-window thinking without replacing Day 6.
- Handle edge cases such as empty strings, spaces, uppercase letters, duplicates, and repeated characters.
- Explain common string and hashing solutions in interviews.

---

# 📌 Prerequisites

You should already know:

- Java variables and data types.
- Loops.
- Conditions.
- Methods.
- Arrays.
- Basic time complexity.
- Basic array traversal.
- Subarrays and contiguous ranges from Day 4.

You should have completed:

- **Day 1 — Java Basics**
- **Day 2 — Number Problems + Patterns**
- **Day 3 — Arrays Fundamentals**
- **Day 4 — Prefix Sum + Subarrays + Kadane**

---

# 🔥 PRIORITY

## 🔥 MUST KNOW

Strings and hashing are extremely common in:

- Placement assessments.
- LeetCode.
- HackerRank.
- Technical interviews.
- Coding rounds.

The central idea today is:

> **If you repeatedly need to ask "Have I seen this before?", "How many times did this occur?", or "Where did this occur?", think about hashing.**

---

# 1. 🧑‍🎓 BEGINNER EXPLANATION — WHAT IS A STRING?

A string is a sequence of characters.

Example:

```text
"hello"
```

Characters:

```text
h e l l o
```

Indices:

```text
0 1 2 3 4
```

Visual:

```text
Index:    0   1   2   3   4
          -------------------
Char:     h   e   l   l   o
```

In Java:

```java
String s = "hello";
```

---

# 2. STRING TERMINOLOGY

| Term | Meaning |
|---|---|
| Character | One symbol such as `a`, `7`, `@` |
| String | Sequence of characters |
| Index | Position of a character |
| Length | Number of characters |
| Substring | Contiguous part of a string |
| Subsequence | Characters kept in order, but gaps allowed |
| Anagram | Strings with the same character counts |
| Palindrome | Reads the same forward and backward |
| Frequency | Number of occurrences |
| Hashing | Using a data structure to support fast lookup |

---

# 3. STRING INDEXING

Given:

```java
String s = "hello";
```

we have:

```text
Index:    0   1   2   3   4
          -------------------
Char:     h   e   l   l   o
```

Therefore:

```java
s.charAt(0) → 'h'
s.charAt(1) → 'e'
s.charAt(4) → 'o'
```

The last valid index is:

```text
s.length() - 1
```

---

# 4. STRING LENGTH

For:

```java
String s = "hello";
```

use:

```java
s.length()
```

Result:

```text
5
```

Remember:

```text
Array → arr.length
String → s.length()
```

This is a very common Java interview/coding-test mistake.

---

# 5. STRING TRAVERSAL

Use:

```java
for (int i = 0; i < s.length(); i++) {

    char ch = s.charAt(i);

    System.out.println(ch);
}
```

For:

```text
"cat"
```

output:

```text
c
a
t
```

Complexity:

```text
Time: O(n)
Space: O(1)
```

assuming character access is constant time for the normal Java `String` operations used here.

---

# 6. `toCharArray()`

You can convert a String into a character array:

```java
char[] chars = s.toCharArray();
```

Example:

```java
String s = "hello";

char[] chars = s.toCharArray();
```

Conceptually:

```text
String:
"hello"

char[]:
['h','e','l','l','o']
```

Then:

```java
for (char ch : chars) {
    System.out.println(ch);
}
```

---

# 7. STRING IS IMMUTABLE

Java Strings are immutable.

That means:

> Once a String object is created, its contents cannot be changed directly.

For example:

```java
String s = "hello";
```

This does not modify the existing String:

```java
s.concat(" world");
```

unless you assign the result:

```java
s = s.concat(" world");
```

---

# 8. WHY IMMUTABILITY MATTERS

Consider:

```java
String s = "";

for (char ch : chars) {
    s += ch;
}
```

Repeated concatenation can create many intermediate String objects.

For repeated modifications, prefer:

```java
StringBuilder
```

---

# 9. STRINGBUILDER

Use:

```java
StringBuilder sb = new StringBuilder();
```

Append:

```java
sb.append("hello");
sb.append(" ");
sb.append("world");
```

Convert to String:

```java
String result = sb.toString();
```

Result:

```text
"hello world"
```

---

# 10. STRINGBUILDER — COMMON OPERATIONS

```java
StringBuilder sb = new StringBuilder();

sb.append("abc");

sb.append('d');

sb.deleteCharAt(1);

sb.reverse();

String result = sb.toString();
```

Commonly useful:

```text
append()
deleteCharAt()
reverse()
toString()
```

---

# 11. STRING COMPARISON — VERY IMPORTANT

Do not use:

```java
s1 == s2
```

to compare String contents.

Use:

```java
s1.equals(s2)
```

Example:

```java
String a = "hello";
String b = new String("hello");

System.out.println(a.equals(b));
```

Output:

```text
true
```

---

# 12. `==` VS `.equals()`

| Operator / Method | What it compares |
|---|---|
| `==` | References |
| `.equals()` | String contents |

For DSA string comparison:

```java
s1.equals(s2)
```

is usually what you want.

---

# 13. CASE SENSITIVITY

```java
"Hello".equals("hello")
```

returns:

```text
false
```

If case-insensitive comparison is specifically required:

```java
"Hello".equalsIgnoreCase("hello")
```

returns:

```text
true
```

Do not change case unless the problem requires it.

---

# 14. SUBSTRING

A substring is a contiguous part of a string.

Example:

```text
"abcdef"
```

Some substrings:

```text
"abc"
"bcd"
"cde"
"def"
"abcd"
```

`"ace"` is not a substring because characters are not contiguous.

---

# 15. `substring()` IN JAVA

```java
String s = "abcdef";

String x = s.substring(1, 4);
```

Result:

```text
"bcd"
```

Important:

```text
start index → inclusive
end index   → exclusive
```

So:

```java
substring(1, 4)
```

means indices:

```text
1, 2, 3
```

---

# 16. SUBSTRING VS SUBSEQUENCE

This is important because Day 4 introduced the same distinction for arrays.

For:

```text
"abcde"
```

Substring:

```text
"bcd"
```

Subsequence:

```text
"ace"
```

because the characters remain in order but do not need to be adjacent.

---

# 17. OTHER USEFUL STRING METHODS

```java
s.charAt(i)
s.length()
s.substring(l, r)
s.equals(t)
s.toCharArray()
s.indexOf('a')
s.contains("abc")
s.startsWith("pre")
s.endsWith("ing")
s.toLowerCase()
s.toUpperCase()
s.trim()
```

Use only what the problem requires.

---

# 18. ⚠️ STRING METHODS AND COMPLEXITY

Be careful about repeatedly creating substrings or concatenating strings inside large loops.

For placement problems, prefer:

```text
One traversal
+
Character checks
+
StringBuilder when constructing output
```

when possible.

---

# 19. 🧑‍🎓 BEGINNER EXPLANATION — WHAT IS HASHING?

Imagine you have:

```text
apple → 3
banana → 5
orange → 2
```

You want to ask:

```text
How many apples?
```

Instead of scanning a list every time, a hash table stores a mapping:

```text
key → value
```

So:

```text
apple → 3
```

can be looked up efficiently on average.

This is the basic idea behind:

```text
HashMap
HashSet
```

---

# 20. WHY DO WE NEED HASHING?

Suppose:

```text
arr = [4, 7, 2, 7, 9, 4, 7]
```

Question:

> How many times does each number appear?

Brute force might repeatedly scan the array.

Hashing lets us maintain:

```text
4 → 2
7 → 3
2 → 1
9 → 1
```

This is a frequency map.

---

# 21. HASHING TERMINOLOGY

| Term | Meaning |
|---|---|
| Key | Identifier used for lookup |
| Value | Information associated with the key |
| HashMap | Key → Value mapping |
| HashSet | Collection of unique values |
| Frequency Map | Key → occurrence count |
| Lookup | Check/retrieve information for a key |
| Insert | Add a key/value |
| Update | Change value associated with a key |
| Duplicate | Key/value appearing again |

---

# 22. HASHMAP IN JAVA

Import:

```java
import java.util.HashMap;
```

Create:

```java
HashMap<Character, Integer> map = new HashMap<>();
```

Store:

```java
map.put('a', 1);
```

Get:

```java
map.get('a');
```

Check:

```java
map.containsKey('a');
```

Remove:

```java
map.remove('a');
```

---

# 23. `getOrDefault()` — VERY IMPORTANT

Instead of:

```java
if (map.containsKey(ch)) {
    map.put(ch, map.get(ch) + 1);
} else {
    map.put(ch, 1);
}
```

you can write:

```java
map.put(ch, map.getOrDefault(ch, 0) + 1);
```

This is one of the most useful Java DSA patterns.

---

# 24. FREQUENCY COUNT — CHARACTER

Problem:

```text
"banana"
```

Count each character.

Expected:

```text
b → 1
a → 3
n → 2
```

Java:

```java
HashMap<Character, Integer> freq = new HashMap<>();

for (char ch : s.toCharArray()) {

    freq.put(
        ch,
        freq.getOrDefault(ch, 0) + 1
    );
}
```

---

# 25. DRY RUN — FREQUENCY MAP

Input:

```text
"banana"
```

Start:

```text
{}
```

`b`:

```text
{b=1}
```

`a`:

```text
{b=1, a=1}
```

`n`:

```text
{b=1, a=1, n=1}
```

`a`:

```text
{b=1, a=2, n=1}
```

`n`:

```text
{b=1, a=2, n=2}
```

`a`:

```text
{b=1, a=3, n=2}
```

Final:

```text
b → 1
a → 3
n → 2
```

---

# 26. HASHSET IN JAVA

A `HashSet` stores unique values.

```java
HashSet<Character> set = new HashSet<>();
```

Add:

```java
set.add('a');
```

Check:

```java
set.contains('a');
```

Remove:

```java
set.remove('a');
```

Size:

```java
set.size();
```

---

# 27. HASHSET VS HASHMAP

| Need | Use |
|---|---|
| Just remember whether something exists | HashSet |
| Count occurrences | HashMap |
| Store key → information | HashMap |
| Store unique values | HashSet |
| Find duplicates | HashSet often works |
| Frequency | HashMap |

Memory trick:

```text
Set = "Have I seen it?"

Map = "What information do I know about it?"
```

---

# 28. HASHING COMPLEXITY

Average-case lookup:

```text
O(1)
```

Average-case insertion:

```text
O(1)
```

Average-case removal:

```text
O(1)
```

Therefore, hashing can transform:

```text
Repeated linear search → average constant-time lookup
```

However, these are average-case expectations, not a mathematical guarantee for every possible input.

---

# 29. EXAMPLE 1 — COUNT VOWELS

Input:

```text
"education"
```

Count:

```text
a,e,i,o,u
```

---

## Java

```java
class Solution {

    public int countVowels(String s) {

        int count = 0;

        for (char ch : s.toCharArray()) {

            if (ch == 'a' ||
                ch == 'e' ||
                ch == 'i' ||
                ch == 'o' ||
                ch == 'u') {

                count++;
            }
        }

        return count;
    }
}
```

---

## Complexity

```text
Time: O(n)
Space: O(1)
```

No HashMap is needed because the set of vowels is fixed and tiny.

---

# 30. 🧠 IMPORTANT PATTERN

Do not use a HashMap just because today's topic is hashing.

Ask:

> **Is the key space small and fixed?**

If yes, an array may be simpler.

Examples:

```text
lowercase English letters → int[26]
digits 0–9 → int[10]
```

This is often faster and simpler.

---

# 31. FREQUENCY ARRAY — LOWERCASE LETTERS

For lowercase English letters:

```text
a b c d ... z
0 1 2 3 ... 25
```

We can map:

```java
int index = ch - 'a';
```

Example:

```java
'a' - 'a' = 0
'b' - 'a' = 1
'z' - 'a' = 25
```

---

# 32. FREQUENCY ARRAY CODE

```java
int[] freq = new int[26];

for (char ch : s.toCharArray()) {

    freq[ch - 'a']++;
}
```

For:

```text
"banana"
```

we get counts for:

```text
a
b
n
```

---

# 33. HASHMAP VS FREQUENCY ARRAY

| Situation | Better simple choice |
|---|---|
| lowercase `a-z` | `int[26]` |
| digits `0-9` | `int[10]` |
| known small alphabet | Frequency array |
| Arbitrary strings | HashMap |
| General objects as keys | HashMap |
| Need unique values | HashSet |

---

# 34. EXAMPLE 2 — VALID ANAGRAM

Problem:

```text
s = "listen"
t = "silent"
```

Are they anagrams?

Answer:

```text
true
```

Anagrams have:

> The same character frequencies.

---

# 35. BRUTE FORCE

One approach:

```text
Sort both strings.
Compare them.
```

Example:

```text
listen → eilnst
silent → eilnst
```

Therefore they match.

Complexity:

```text
O(n log n)
```

---

# 36. OPTIMAL — FREQUENCY COUNTING

Instead of sorting:

```text
Count characters in s
Subtract/count characters in t
```

For lowercase English letters, use:

```java
int[26]
```

---

## Java

```java
class Solution {

    public boolean isAnagram(String s, String t) {

        if (s.length() != t.length()) {
            return false;
        }

        int[] freq = new int[26];

        for (char ch : s.toCharArray()) {
            freq[ch - 'a']++;
        }

        for (char ch : t.toCharArray()) {
            freq[ch - 'a']--;
        }

        for (int count : freq) {

            if (count != 0) {
                return false;
            }
        }

        return true;
    }
}
```

---

# 37. DRY RUN — ANAGRAM

```text
s = "listen"
t = "silent"
```

After processing `s`, frequencies are:

```text
l → 1
i → 1
s → 1
t → 1
e → 1
n → 1
```

Process `t`.

Each corresponding count returns to zero.

Final:

```text
all frequencies = 0
```

Therefore:

```text
true
```

---

# 38. COMPLEXITY — ANAGRAM

```text
Time: O(n)
Space: O(1)
```

Why `O(1)` space?

Because:

```text
int[26]
```

has fixed size regardless of `n`.

---

# 39. ⚠️ ANAGRAM EDGE CASES

Consider:

```text
""
""
```

Usually true.

Different lengths:

```text
"abc"
"ab"
```

Immediately false.

Case:

```text
"Ab"
"ba"
```

Whether this is an anagram depends on the problem's case rules.

Do not silently normalize unless required.

---

# 40. HASHMAP VERSION OF ANAGRAM

If the character set is not limited to lowercase English letters:

```java
HashMap<Character, Integer> freq = new HashMap<>();
```

Then:

```java
for (char ch : s.toCharArray()) {
    freq.put(ch, freq.getOrDefault(ch, 0) + 1);
}

for (char ch : t.toCharArray()) {

    if (!freq.containsKey(ch)) {
        return false;
    }

    freq.put(ch, freq.get(ch) - 1);

    if (freq.get(ch) == 0) {
        freq.remove(ch);
    }
}
```

This is useful when the alphabet is not fixed to `a-z`.

---

# 41. EXAMPLE 3 — FIRST UNIQUE CHARACTER

Problem:

```text
"leetcode"
```

Return the index of the first character that occurs exactly once.

Answer:

```text
0
```

because:

```text
l
```

appears once.

---

# 42. BRUTE FORCE

For each character:

```text
count how many times it appears
```

If we scan the whole string for every character:

```text
O(n²)
```

---

# 43. OPTIMAL — TWO PASSES + FREQUENCY

Pass 1:

```text
Count every character.
```

Pass 2:

```text
Find the first character whose count is 1.
```

Complexity:

```text
O(n)
```

---

## Java

```java
class Solution {

    public int firstUniqChar(String s) {

        int[] freq = new int[26];

        for (char ch : s.toCharArray()) {
            freq[ch - 'a']++;
        }

        for (int i = 0; i < s.length(); i++) {

            if (freq[s.charAt(i) - 'a'] == 1) {
                return i;
            }
        }

        return -1;
    }
}
```

---

# 44. DRY RUN — FIRST UNIQUE

Input:

```text
"loveleetcode"
```

Frequency:

```text
l → 2
o → 2
v → 1
e → 4
...
```

Scan from left:

```text
l → repeated
o → repeated
v → unique
```

Return:

```text
2
```

---

# 45. COMPLEXITY

```text
Time: O(n)
Space: O(1)
```

for lowercase English letters.

The standard problem asks for the first non-repeating character's index and returns `-1` if none exists. citeturn0search3

---

# 46. EXAMPLE 4 — FIND DUPLICATE CHARACTER

Problem:

```text
"programming"
```

Find whether any character appears more than once.

---

## HashSet approach

```java
class Solution {

    public boolean hasDuplicate(String s) {

        HashSet<Character> set = new HashSet<>();

        for (char ch : s.toCharArray()) {

            if (set.contains(ch)) {
                return true;
            }

            set.add(ch);
        }

        return false;
    }
}
```

---

## Complexity

Average:

```text
Time: O(n)
Space: O(n)
```

---

# 47. WHY HASHSET?

We only need to know:

```text
Have I seen this character before?
```

We do not need its count.

Therefore:

```text
HashSet
```

is a natural fit.

---

# 48. EXAMPLE 5 — TWO SUM

This is one of the most important HashMap patterns.

Given:

```text
nums = [2,7,11,15]
target = 9
```

Answer:

```text
[0,1]
```

because:

```text
2 + 7 = 9
```

---

# 49. BRUTE FORCE — TWO SUM

Check every pair:

```text
i
j
```

Complexity:

```text
O(n²)
```

---

# 50. KEY OBSERVATION

Suppose current value is:

```text
x
```

We need:

```text
target - x
```

This is called the:

> **complement**

Example:

```text
target = 9
x = 2

complement = 9 - 2 = 7
```

So we ask:

```text
Have I already seen 7?
```

A HashMap can answer that efficiently.

---

# 51. TWO SUM — HASHMAP

Store:

```text
value → index
```

As we scan:

```text
2 → 0
```

At `7`:

```text
complement = 9 - 7 = 2
```

`2` is already in the map.

Therefore:

```text
[0,1]
```

---

## Java

```java
class Solution {

    public int[] twoSum(int[] nums, int target) {

        HashMap<Integer, Integer> map = new HashMap<>();

        for (int i = 0; i < nums.length; i++) {

            int complement = target - nums[i];

            if (map.containsKey(complement)) {
                return new int[]{
                    map.get(complement),
                    i
                };
            }

            map.put(nums[i], i);
        }

        return new int[]{-1, -1};
    }
}
```

---

# 52. DRY RUN — TWO SUM

Input:

```text
nums = [2,7,11,15]
target = 9
```

Start:

```text
map = {}
```

### `i = 0`

```text
nums[i] = 2
complement = 7
```

7 not found.

Store:

```text
{2=0}
```

### `i = 1`

```text
nums[i] = 7
complement = 2
```

2 found at index `0`.

Return:

```text
[0,1]
```

---

# 53. COMPLEXITY — TWO SUM

```text
Time: O(n) average
Space: O(n)
```

Compared with:

```text
Brute Force → O(n²)
HashMap → O(n) average
```

This is one of the most important brute-force-to-hashing transformations.

---

# 54. ⚠️ TWO SUM DUPLICATE CASE

Input:

```text
[3,3]
target = 6
```

At first `3`:

```text
map = {3=0}
```

At second `3`:

```text
complement = 3
```

It is already present.

Return:

```text
[0,1]
```

This works because we store earlier elements.

---

# 55. 🧠 HASHING PATTERN — COMPLEMENT

Whenever you see:

> Find two values satisfying a target relationship.

Ask:

```text
If current = x,
what value do I need?
```

For sum:

```text
needed = target - x
```

Then:

```text
Have I seen needed?
```

This idea generalizes beyond Two Sum.

---

# 56. HASHMAP FREQUENCY TEMPLATE

```java
HashMap<Character, Integer> freq = new HashMap<>();

for (char ch : s.toCharArray()) {

    freq.put(
        ch,
        freq.getOrDefault(ch, 0) + 1
    );
}
```

Remember:

```text
Key   = thing being counted
Value = count
```

---

# 57. HASHSET SEEN TEMPLATE

```java
HashSet<Character> seen = new HashSet<>();

for (char ch : s.toCharArray()) {

    if (seen.contains(ch)) {
        // duplicate
    }

    seen.add(ch);
}
```

Remember:

```text
Set = have I seen it?
```

---

# 58. HASHMAP INDEX TEMPLATE

```java
HashMap<Integer, Integer> map = new HashMap<>();

for (int i = 0; i < nums.length; i++) {

    map.put(nums[i], i);
}
```

Remember:

```text
value → index
```

This is useful for:

- Two Sum.
- Last occurrence.
- Position lookup.
- Duplicate-related problems.

---

# 59. HASHMAP — LAST OCCURRENCE

Suppose:

```text
s = "abca"
```

We want the last index of each character.

```java
HashMap<Character, Integer> last = new HashMap<>();

for (int i = 0; i < s.length(); i++) {
    last.put(s.charAt(i), i);
}
```

Final:

```text
a → 3
b → 1
c → 2
```

Why does this work?

Because later `put()` operations replace the earlier index.

---

# 60. 🧠 HASHING PATTERN RECOGNITION

Think hashing when the problem says:

- Count frequencies.
- Find duplicates.
- Check whether something exists.
- Find first/last occurrence.
- Find pairs.
- Find complement.
- Group equal/similar objects.
- Remember something seen earlier.
- Track a value's index.
- Find repeated elements efficiently.

Ask:

```text
Am I repeatedly searching for something?
        ↓
Can I store what I have already seen?
        ↓
HashMap / HashSet
```

---

# 61. HASHING — WHEN NOT TO USE IT

Do not automatically use hashing.

Examples:

### Fixed lowercase alphabet

Use:

```text
int[26]
```

instead of a HashMap when appropriate.

### Sorted array + two-value target

Two pointers may use:

```text
O(1)
```

extra space.

### Need ordering

HashMap/HashSet do not automatically provide sorted ordering.

Use an appropriate ordered structure if required.

---

# 62. HASHMAP VS TREEMAP — BASIC AWARENESS

| Feature | HashMap | TreeMap |
|---|---|---|
| Average lookup | `O(1)` | `O(log n)` |
| Maintains sorted key order | No | Yes |
| Main idea | Hashing | Balanced tree |
| Typical use | Fast lookup | Ordered keys |

You do not need to master TreeMap today.

Just recognize why HashMap is usually chosen for pure lookup/counting.

---

# 63. HASHSET VS TREESET — BASIC AWARENESS

| Feature | HashSet | TreeSet |
|---|---|---|
| Average lookup | `O(1)` | `O(log n)` |
| Sorted order | No | Yes |
| Duplicates | Not allowed | Not allowed |
| Typical use | Fast uniqueness | Sorted uniqueness |

---

# 64. STRING + HASHING — ANAGRAM PATTERN

```text
Two strings
      ↓
Need same character frequencies?
      ↓
Count characters
      ↓
Compare counts
      ↓
Anagram
```

---

# 65. STRING + HASHING — UNIQUE CHARACTER PATTERN

```text
Need first non-repeating character?
      ↓
Count frequencies
      ↓
Scan original string again
      ↓
First frequency == 1
```

Why two passes?

Because while reading the first occurrence, you may not yet know whether that character will appear later.

---

# 66. STRING + HASHSET — DUPLICATE PATTERN

```text
Need to know whether something repeats?
      ↓
HashSet
      ↓
If already present
      ↓
Duplicate found
```

---

# 67. STRING + HASHMAP — LAST POSITION

```text
Need latest occurrence?
      ↓
Map character → index
      ↓
Overwrite previous index
```

---

# 68. 🧠 INTRODUCTION — STRING + SLIDING WINDOW

Day 6 will cover Sliding Window deeply.

But strings are where you will see it frequently.

Example:

> Find the length of the longest substring without repeating characters.

Input:

```text
"abcabcbb"
```

Answer:

```text
3
```

One valid longest substring is:

```text
"abc"
```

This problem combines:

```text
String
+
Hashing
+
Sliding Window
```

The official LeetCode problem defines the task as finding the longest substring without duplicate characters. citeturn0search5

---

# 69. WHY BRUTE FORCE IS SLOW

A brute-force approach may:

```text
Generate every substring
Check whether each substring contains duplicates
```

There are:

```text
O(n²)
```

substrings.

If duplicate checking takes another `O(n)`, the approach can become:

```text
O(n³)
```

---

# 70. KEY IDEA

Maintain a window:

```text
[left ... right]
```

and a structure containing characters currently inside it.

When a duplicate appears:

```text
move left
```

until the window becomes valid again.

This is the beginning of Sliding Window.

Do not worry if it feels new.

Day 6 will cover it step by step.

---

# 71. HASHMAP VERSION — LONGEST SUBSTRING WITHOUT REPEATING

A useful optimized form stores the latest index of each character.

```java
class Solution {

    public int lengthOfLongestSubstring(String s) {

        HashMap<Character, Integer> lastSeen = new HashMap<>();

        int left = 0;
        int maxLength = 0;

        for (int right = 0; right < s.length(); right++) {

            char ch = s.charAt(right);

            if (lastSeen.containsKey(ch)) {
                left = Math.max(left, lastSeen.get(ch) + 1);
            }

            lastSeen.put(ch, right);

            maxLength = Math.max(
                maxLength,
                right - left + 1
            );
        }

        return maxLength;
    }
}
```

Complexity:

```text
Time: O(n) average
Space: O(k)
```

where `k` is the number of distinct characters tracked.

---

# 72. DRY RUN — LONGEST UNIQUE SUBSTRING

Input:

```text
"abcabcbb"
```

Start:

```text
left = 0
```

Read:

```text
a → window "a" → length 1
b → "ab" → 2
c → "abc" → 3
```

Next:

```text
a
```

Previous `a` was at index `0`.

Move:

```text
left = 1
```

Window:

```text
"bca"
```

Length remains:

```text
3
```

The process continues.

Answer:

```text
3
```

---

# 73. ⚠️ IMPORTANT WINDOW MISTAKE

Wrong:

```java
left = lastSeen.get(ch) + 1;
```

without protecting against moving `left` backward.

Correct:

```java
left = Math.max(
    left,
    lastSeen.get(ch) + 1
);
```

Why?

Because the left pointer should only move forward.

This exact pattern becomes important in Day 6.

---

# 74. BRUTE FORCE → HASHING

Suppose:

> Find the first duplicate character.

### Brute force

For every character:

```text
search later characters
```

Potential:

```text
O(n²)
```

### HashSet

Maintain:

```text
seen
```

Each lookup is average `O(1)`.

Total:

```text
O(n)
```

This is a classic hashing optimization.

---

# 75. BRUTE FORCE → HASHMAP

Suppose:

> Find the number of occurrences of every character.

### Brute force

For every distinct character:

```text
scan the string
```

Potentially:

```text
O(n²)
```

### HashMap

Single scan:

```java
map.put(ch, map.getOrDefault(ch, 0) + 1);
```

Total:

```text
O(n)
```

---

# 76. 🧠 CONSTRAINT THINKING

Suppose:

```text
n <= 100
```

A simple `O(n²)` solution may be acceptable.

Suppose:

```text
n <= 100,000
```

look for:

```text
O(n)
O(n log n)
```

If the problem asks for:

```text
frequency
duplicate
existence
pair
```

hashing is often worth investigating.

---

# 77. EDGE CASE MASTER LIST — STRINGS

Always test:

### Empty

```text
""
```

### One character

```text
"a"
```

### All same

```text
"aaaaa"
```

### All unique

```text
"abcdef"
```

### Repeated at beginning

```text
"aabc"
```

### Repeated at end

```text
"abca"
```

### Spaces

```text
"a b a"
```

### Uppercase

```text
"AbA"
```

### Digits

```text
"a1a"
```

### Special characters

```text
"a@a"
```

### Unicode

Only handle it specially when the problem's character model requires it.

---

# 78. JAVA-SPECIFIC STRING MISTAKES

## Mistake 1

Wrong:

```java
s.length
```

Correct:

```java
s.length()
```

---

## Mistake 2

Wrong:

```java
s[i]
```

Correct:

```java
s.charAt(i)
```

---

## Mistake 3

Wrong:

```java
s1 == s2
```

for content comparison.

Correct:

```java
s1.equals(s2)
```

---

## Mistake 4

Repeated:

```java
result += ch;
```

inside a large loop.

Prefer:

```java
StringBuilder
```

when repeated construction is needed.

---

## Mistake 5

Assuming lowercase input when the problem does not guarantee it.

If the input can contain:

```text
A-Z
a-z
digits
spaces
symbols
```

your frequency strategy must match that requirement.

---

# 79. JAVA-SPECIFIC HASHING MISTAKES

## Mistake 1

Forgetting:

```java
import java.util.HashMap;
import java.util.HashSet;
```

---

## Mistake 2

Calling:

```java
map.get(key) + 1
```

when the key may not exist.

Prefer:

```java
map.getOrDefault(key, 0) + 1
```

---

## Mistake 3

Using `HashSet` when you actually need counts.

Use:

```text
HashMap
```

for frequencies.

---

## Mistake 4

Using HashMap when `int[26]` is simpler.

---

## Mistake 5

Assuming HashMap provides sorted order.

It is a lookup structure, not a sorting tool.

---

# 80. PATTERN COMPARISON

| Problem clue | First pattern to consider |
|---|---|
| Count characters | Frequency array / HashMap |
| Character from `a-z` | `int[26]` |
| Have I seen this? | HashSet |
| How many times? | HashMap |
| Where was it last? | HashMap |
| Two values sum to target | HashMap complement |
| Same frequencies? | Anagram counting |
| First unique | Frequency + second scan |
| Longest unique substring | Hashing + Sliding Window |
| Sorted pair sum | Two pointers |
| Range sum | Prefix Sum |

---

# 81. 🎤 INTERVIEW EXPLANATION — HASHING

A strong general answer:

> "I use hashing when I need fast average-case lookup for information I've already seen. Instead of repeatedly scanning the input, I store keys in a HashSet or key-value information in a HashMap. This often reduces a nested-loop solution from O(n²) to O(n) at the cost of additional space."

---

# 82. 🎤 INTERVIEW EXPLANATION — FREQUENCY MAP

> "I traverse the string once and maintain a frequency for every character. The character is the key and the count is the value. Using `getOrDefault` lets me increment the count safely. This gives O(n) average time."

---

# 83. 🎤 INTERVIEW EXPLANATION — TWO SUM

> "The brute-force solution checks every pair in O(n²). For each number x, I know I need target minus x. I store previously seen values and their indices in a HashMap. When the complement already exists, I can immediately return the two indices. This gives O(n) average time and O(n) extra space."

---

# 84. 🧪 MINI PRACTICE — STRING BASICS

## Problem 1

Print every character of:

```text
"hello"
```

<details>
<summary>💡 Hint</summary>

Use:

```java
s.charAt(i)
```

</details>

<details>
<summary>✅ Solution</summary>

```java
for (int i = 0; i < s.length(); i++) {
    System.out.println(s.charAt(i));
}
```

Complexity:

```text
Time: O(n)
Space: O(1)
```

</details>

---

## Problem 2

Count the number of uppercase letters.

Input:

```text
"HelloWORLD"
```

<details>
<summary>💡 Hint</summary>

Use:

```java
Character.isUpperCase(ch)
```

</details>

<details>
<summary>✅ Solution</summary>

```java
int count = 0;

for (char ch : s.toCharArray()) {

    if (Character.isUpperCase(ch)) {
        count++;
    }
}

return count;
```

</details>

---

# 85. 🧪 MINI PRACTICE — FREQUENCY

## Problem 1

Count characters in:

```text
"apple"
```

<details>
<summary>💡 Hint</summary>

Use a `HashMap<Character, Integer>`.

</details>

<details>
<summary>✅ Solution</summary>

```java
HashMap<Character, Integer> map = new HashMap<>();

for (char ch : s.toCharArray()) {
    map.put(ch, map.getOrDefault(ch, 0) + 1);
}
```

Expected:

```text
a → 1
p → 2
l → 1
e → 1
```

</details>

---

## Problem 2

Check whether:

```text
"programming"
```

contains a duplicate character.

<details>
<summary>💡 Hint</summary>

Use a `HashSet`.

</details>

<details>
<summary>✅ Solution</summary>

```java
HashSet<Character> seen = new HashSet<>();

for (char ch : s.toCharArray()) {

    if (seen.contains(ch)) {
        return true;
    }

    seen.add(ch);
}

return false;
```

</details>

---

# 86. 🧪 MINI PRACTICE — HASHMAP

## Problem 1

Find the first character that occurs exactly once.

```text
"swiss"
```

<details>
<summary>💡 Hint</summary>

Use two passes:

1. Count.
2. Scan again.

</details>

<details>
<summary>✅ Solution</summary>

```java
HashMap<Character, Integer> freq = new HashMap<>();

for (char ch : s.toCharArray()) {
    freq.put(ch, freq.getOrDefault(ch, 0) + 1);
}

for (int i = 0; i < s.length(); i++) {

    if (freq.get(s.charAt(i)) == 1) {
        return i;
    }
}

return -1;
```

For `"swiss"`:

```text
w
```

is the first unique character.

</details>

---

## Problem 2

Find whether:

```text
"listen"
"silent"
```

are anagrams.

<details>
<summary>💡 Hint</summary>

Their frequency counts must be identical.

</details>

<details>
<summary>✅ Solution</summary>

```java
if (s.length() != t.length()) {
    return false;
}

int[] freq = new int[26];

for (char ch : s.toCharArray()) {
    freq[ch - 'a']++;
}

for (char ch : t.toCharArray()) {
    freq[ch - 'a']--;
}

for (int count : freq) {

    if (count != 0) {
        return false;
    }
}

return true;
```

</details>

---

# 87. 🧪 MINI PRACTICE — TWO SUM

## Problem

```text
nums = [2,7,11,15]
target = 9
```

<details>
<summary>💡 Hint</summary>

For each `x`:

```text
needed = target - x
```

Store previous values and indices.

</details>

<details>
<summary>✅ Solution</summary>

```java
HashMap<Integer, Integer> map = new HashMap<>();

for (int i = 0; i < nums.length; i++) {

    int needed = target - nums[i];

    if (map.containsKey(needed)) {
        return new int[]{
            map.get(needed),
            i
        };
    }

    map.put(nums[i], i);
}

return new int[]{-1, -1};
```

Complexity:

```text
Time: O(n) average
Space: O(n)
```

</details>

---

# 88. FULL PRACTICE PROBLEM — VALID ANAGRAM

## Problem

```text
s = "anagram"
t = "nagaram"
```

Return:

```text
true
```

---

## Step 1 — Brute Force

Sort both strings.

```text
anagram → aaagmnr
nagaram → aaagmnr
```

Time:

```text
O(n log n)
```

---

## Step 2 — Observation

Anagrams have identical character frequencies.

---

## Step 3 — Optimal

```java
class Solution {

    public boolean isAnagram(String s, String t) {

        if (s.length() != t.length()) {
            return false;
        }

        int[] freq = new int[26];

        for (char ch : s.toCharArray()) {
            freq[ch - 'a']++;
        }

        for (char ch : t.toCharArray()) {
            freq[ch - 'a']--;
        }

        for (int count : freq) {

            if (count != 0) {
                return false;
            }
        }

        return true;
    }
}
```

---

## Dry Run

```text
s = anagram
t = nagaram
```

Every character count balances.

Final:

```text
all 0
```

Answer:

```text
true
```

---

## Complexity

```text
Time: O(n)
Space: O(1)
```

for lowercase English letters.

---

# 89. FULL PRACTICE PROBLEM — FIRST UNIQUE CHARACTER

## Input

```text
"loveleetcode"
```

Expected:

```text
2
```

---

## Brute Force

For every character, count occurrences.

```text
O(n²)
```

---

## Optimal

Frequency array:

```text
O(n)
```

Java:

```java
class Solution {

    public int firstUniqChar(String s) {

        int[] freq = new int[26];

        for (char ch : s.toCharArray()) {
            freq[ch - 'a']++;
        }

        for (int i = 0; i < s.length(); i++) {

            if (freq[s.charAt(i) - 'a'] == 1) {
                return i;
            }
        }

        return -1;
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

# 90. FULL PRACTICE PROBLEM — TWO SUM

## Input

```text
nums = [3,2,4]
target = 6
```

Output:

```text
[1,2]
```

---

## Brute Force

Check pairs:

```text
3 + 2 = 5
3 + 4 = 7
2 + 4 = 6
```

Complexity:

```text
O(n²)
```

---

## HashMap

For `3`:

```text
needed = 3
map = {}
```

Store:

```text
3 → 0
```

For `2`:

```text
needed = 4
```

Not found.

Store:

```text
2 → 1
```

For `4`:

```text
needed = 2
```

Found:

```text
2 → index 1
```

Return:

```text
[1,2]
```

---

## Complexity

```text
Time: O(n) average
Space: O(n)
```

The official LeetCode problem specifies that the input has exactly one valid solution and asks for the two indices. citeturn0search2

---

# 91. FULL PRACTICE PROBLEM — LONGEST UNIQUE SUBSTRING

## Input

```text
"abcabcbb"
```

Output:

```text
3
```

---

## Brute Force

Generate substrings and check uniqueness.

Potential:

```text
O(n³)
```

---

## Better

Use a Set and sliding window.

---

## Optimal HashMap + Window

```java
class Solution {

    public int lengthOfLongestSubstring(String s) {

        HashMap<Character, Integer> lastSeen = new HashMap<>();

        int left = 0;
        int maxLength = 0;

        for (int right = 0; right < s.length(); right++) {

            char ch = s.charAt(right);

            if (lastSeen.containsKey(ch)) {
                left = Math.max(
                    left,
                    lastSeen.get(ch) + 1
                );
            }

            lastSeen.put(ch, right);

            maxLength = Math.max(
                maxLength,
                right - left + 1
            );
        }

        return maxLength;
    }
}
```

---

## Complexity

```text
Time: O(n) average
Space: O(k)
```

where `k` is the number of distinct characters tracked.

The official problem is classified with Hash Table, String, and Sliding Window concepts and uses examples such as `"abcabcbb" → 3`. citeturn0search0turn0search5

---

# 92. PATTERN COMPARISON — FREQUENCY ARRAY VS HASHMAP

| Feature | Frequency Array | HashMap |
|---|---|---|
| Fixed alphabet | Excellent | Works |
| Arbitrary characters | Limited | Better |
| Lowercase `a-z` | `O(1)` fixed space | `O(k)` |
| Syntax | Very simple | More verbose |
| Memory | Fixed | Depends on keys |
| Typical use | Character frequency | General lookup |

---

# 93. PATTERN COMPARISON — HASHSET VS HASHMAP

| Question | Use |
|---|---|
| Have I seen it? | HashSet |
| How many times? | HashMap |
| What index did I see? | HashMap |
| What information is associated with it? | HashMap |
| Need unique values only? | HashSet |

---

# 94. PATTERN COMPARISON — SORTING VS HASHING

Suppose you need to check whether two strings are anagrams.

### Sorting

```text
Sort s
Sort t
Compare
```

Complexity:

```text
O(n log n)
```

### Frequency counting

```text
Count characters
```

Complexity:

```text
O(n)
```

when the alphabet is fixed.

This is a common optimization pattern:

```text
Ordering information
       vs
Frequency information
```

Choose what the problem actually needs.

---

# 95. 🧠 HASHING DECISION TREE

```text
Need information about previous values?
             |
            YES
             |
     +-------+-------+
     |               |
 Need count?      Need existence?
     |               |
 HashMap          HashSet
     |
     +----------------------+
     |                      |
 Need index?           Need frequency?
     |                      |
 HashMap               HashMap /
                        freq array
```

---

# 96. CONSTRAINT THINKING

If:

```text
n ≤ 100
```

a simple nested loop may be acceptable.

If:

```text
n ≤ 100,000
```

look for:

```text
O(n)
```

If the character set is:

```text
a-z
```

consider:

```text
int[26]
```

If the problem allows arbitrary characters or keys:

```text
HashMap
```

If only existence matters:

```text
HashSet
```

---

# 97. 📝 DAILY QUIZ — 10 QUESTIONS

## Q1 — MCQ

How do you get the length of a Java String?

A. `s.length`  
B. `s.length()`  
C. `s.size()`  
D. `s.count()`

---

## Q2 — MCQ

How do you safely compare String contents?

A. `==`  
B. `equals()`  
C. `compare`  
D. `same()`

---

## Q3 — MCQ

Which data structure is best when you only need to know whether an item has been seen?

A. HashSet  
B. HashMap  
C. Stack  
D. Queue

---

## Q4 — MCQ

Which structure is natural for character frequencies?

A. HashMap  
B. HashSet  
C. Stack  
D. Queue

---

## Q5 — Output

What is:

```java
String s = "hello";
System.out.println(s.charAt(1));
```

A. `h`  
B. `e`  
C. `l`  
D. `o`

---

## Q6 — Concept

For lowercase English letters, what fixed-size frequency array can be used?

A. `int[10]`  
B. `int[26]`  
C. `int[52]`  
D. `int[128]`

---

## Q7 — Pattern Recognition

For Two Sum, what value do we search for when the current number is `x`?

A. `x + target`  
B. `target - x`  
C. `x * target`  
D. `target / x`

---

## Q8 — Complexity

What is the average-case time complexity of a single HashMap lookup?

A. `O(n)`  
B. `O(log n)`  
C. `O(1)`  
D. `O(n²)`

---

## Q9 — Debugging

What is wrong with:

```java
if (s1 == s2)
```

when the goal is to compare String contents?

---

## Q10 — Pattern Recognition

You need the first non-repeating character.

Which approach is most natural?

A. Count frequencies, then scan again  
B. Sort the string only  
C. Binary Search  
D. DFS

---

# 98. 📝 ANSWER KEY

### Q1

**B — `s.length()`**

### Q2

**B — `equals()`**

### Q3

**A — HashSet**

### Q4

**A — HashMap**

For lowercase English letters, a frequency array is also often even simpler.

### Q5

**B — `e`**

### Q6

**B — `int[26]`**

### Q7

**B — `target - x`**

### Q8

**C — `O(1)` average**

### Q9

`==` compares object references, not String contents.

Use:

```java
s1.equals(s2)
```

### Q10

**A — Count frequencies, then scan again**

---

# 99. 🧪 PATTERN RECOGNITION TEST

Classify the following before coding.

### 1.

> Count how many times each lowercase letter appears.

**Think:** `int[26]`.

### 2.

> Determine whether an array contains duplicates.

**Think:** HashSet.

### 3.

> Count how many times each integer appears.

**Think:** HashMap.

### 4.

> Find the index of the first non-repeating character.

**Think:** Frequency + second scan.

### 5.

> Find two numbers that sum to target.

**Think:** HashMap complement.

### 6.

> Two strings contain the same character frequencies.

**Think:** Anagram / frequency counting.

### 7.

> Find the last position of each character.

**Think:** HashMap character → index.

### 8.

> Longest substring without repeating characters.

**Think:** Hashing + Sliding Window.

### 9.

> Sorted array and target pair.

**Think:** Two Pointers may be possible; Day 6/previous patterns apply.

### 10.

> Repeated range sum.

**Think:** Prefix Sum, not hashing by default.

---

# 100. 🧠 30-SECOND REVISION

## String

```java
s.length()
s.charAt(i)
s.substring(l, r)
s.equals(t)
s.toCharArray()
```

## StringBuilder

```java
StringBuilder sb = new StringBuilder();

sb.append(ch);

String result = sb.toString();
```

## HashMap

```java
HashMap<K, V> map = new HashMap<>();
```

Frequency:

```java
map.put(
    key,
    map.getOrDefault(key, 0) + 1
);
```

## HashSet

```java
HashSet<T> set = new HashSet<>();

if (set.contains(x)) {
    // seen
}

set.add(x);
```

## Lowercase frequency

```java
int[] freq = new int[26];

freq[ch - 'a']++;
```

## Two Sum

```java
int needed = target - nums[i];

if (map.containsKey(needed)) {
    return new int[]{map.get(needed), i};
}

map.put(nums[i], i);
```

---

# 101. 🧠 MEMORY TRICKS

### HashSet

> **"Have I seen this?"**

### HashMap

> **"What do I know about this?"**

### Frequency Array

> **"The possible keys are small and fixed."**

### Two Sum

> **"What complement do I need?"**

```text
target - current
```

### Anagram

> **"Same counts."**

### First Unique

> **"Count first, scan second."**

---

# 102. 🏠 HOMEWORK

## Must Solve

1. LeetCode — Valid Anagram.
2. LeetCode — First Unique Character in a String.
3. LeetCode — Two Sum.
4. LeetCode — Group Anagrams.
5. LeetCode — Longest Substring Without Repeating Characters.
6. Implement character frequency using `int[26]`.
7. Implement character frequency using `HashMap`.
8. Implement duplicate detection using `HashSet`.
9. Implement Two Sum from memory.
10. Explain why HashMap changes the Two Sum solution from `O(n²)` to `O(n)` average.

## Optional

11. Find the most frequent character.
12. Find the first repeated character.
13. Find the last non-repeating character.
14. Check whether two strings are anagrams using a HashMap.
15. Implement longest unique substring using a HashSet before learning the optimized HashMap version deeply.

---

# 103. 📚 PRACTICE PROBLEMS

## 🟢 Easy

### 1. Valid Anagram

**Platform:** LeetCode  
**Difficulty:** Easy  
**Pattern:** Frequency counting  
**Why:** Teaches the core idea that anagrams have identical character frequencies.  
**What to notice:** With lowercase English letters, `int[26]` is enough.  
**Expected Complexity:** `O(n)` time, `O(1)` extra space for the fixed alphabet.

https://leetcode.com/problems/valid-anagram/ citeturn0search1

---

### 2. First Unique Character in a String

**Platform:** LeetCode  
**Difficulty:** Easy  
**Pattern:** Frequency + second scan  
**Why:** Teaches why one pass may not be enough when future occurrences matter.  
**Expected Complexity:** `O(n)` time, `O(1)` extra space for lowercase English letters.

https://leetcode.com/problems/first-unique-character-in-a-string/ citeturn0search3

---

### 3. Two Sum

**Platform:** LeetCode  
**Difficulty:** Easy  
**Pattern:** HashMap + complement  
**Why:** One of the most important introductory hashing problems.  
**What to notice:** Store previously seen values and their indices.  
**Expected Complexity:** `O(n)` average time, `O(n)` space.

https://leetcode.com/problems/two-sum/ citeturn0search2

---

## 🟡 Medium

### 4. Group Anagrams

**Platform:** LeetCode  
**Difficulty:** Medium  
**Pattern:** HashMap + canonical key  
**Why:** Teaches how multiple strings can be grouped using a shared representation.  
**What to notice:** Anagrams can share the same sorted-character key or frequency signature.  
**Expected Complexity:** Depends on the key construction; sorting-based keys are typically `O(n * k log k)` for `n` strings of average length `k`.

https://leetcode.com/problems/group-anagrams/ citeturn0search6

---

### 5. Longest Substring Without Repeating Characters

**Platform:** LeetCode  
**Difficulty:** Medium  
**Pattern:** HashMap + Sliding Window  
**Why:** Important bridge from hashing to the Day 6 Sliding Window topic.  
**What to notice:** Track the latest index and move the left boundary forward.  
**Expected Complexity:** `O(n)` average time.

https://leetcode.com/problems/longest-substring-without-repeating-characters/ citeturn0search5

---

# 104. PRACTICE ORDER

Follow this order:

```text
1. Valid Anagram
        ↓
2. First Unique Character
        ↓
3. Two Sum
        ↓
4. Group Anagrams
        ↓
5. Longest Substring Without Repeating Characters
```

Do not rush into advanced HashMap problems.

First become comfortable with:

```text
frequency
existence
index
complement
```

---

# 105. 🎤 FINAL INTERVIEW CHEAT SHEET

If interviewer asks:

### "Why HashMap?"

Say:

> "I need fast average-case lookup of information I've already seen."

### "Why HashSet?"

Say:

> "I only need to know whether a value has appeared before; I don't need an associated count or value."

### "Why frequency array instead of HashMap?"

Say:

> "The character set is small and fixed, so a fixed-size array is simpler and uses constant extra space."

### "Why Two Sum with HashMap?"

Say:

> "For each current value x, the required complement is target minus x. I store previous values and their indices so I can find the complement in average O(1)."

### "Why two passes for first unique?"

Say:

> "I need complete frequency information before I can know whether the first occurrence is actually unique."

---

# 106. 🚨 DAY 5 MOST IMPORTANT LESSON

Do not memorize:

```text
HashMap code
HashSet code
```

as isolated syntax.

Understand the question:

```text
What information do I need?
```

If the answer is:

```text
Have I seen it?
```

think:

```text
HashSet
```

If the answer is:

```text
How many times?
```

think:

```text
HashMap / frequency array
```

If the answer is:

```text
Where did I see it?
```

think:

```text
HashMap → value/index
```

If the answer is:

```text
What value do I need to complete this target?
```

think:

```text
Complement
```

If the answer is:

```text
Do these strings have the same counts?
```

think:

```text
Anagram / frequency
```

---

# 107. 🏆 DAY 5 COMPLETION CHECKLIST

- [ ] I understand Java String indexing.
- [ ] I know `s.length()`.
- [ ] I know `s.charAt(i)`.
- [ ] I know `substring(l,r)`.
- [ ] I know why Strings are immutable.
- [ ] I can use StringBuilder.
- [ ] I compare String contents using `.equals()`.
- [ ] I understand substring vs subsequence.
- [ ] I understand hashing.
- [ ] I know HashMap.
- [ ] I know HashSet.
- [ ] I know `getOrDefault()`.
- [ ] I can count frequencies.
- [ ] I can use `int[26]`.
- [ ] I know when to use frequency array vs HashMap.
- [ ] I can detect duplicates with HashSet.
- [ ] I can find first unique character.
- [ ] I can check anagrams.
- [ ] I can solve Two Sum using HashMap.
- [ ] I understand complement.
- [ ] I understand the basic string + sliding-window idea.
- [ ] I understand brute force → hashing optimization.
- [ ] I completed the quiz.
- [ ] I attempted the practice problems.

---

# 108. 🔁 FINAL QUICK WALKTHROUGH

When you get a String/Hashing problem:

```text
STRING / DATA
      ↓
What exactly do I need?
      ↓
Need characters?
      → charAt / toCharArray
      ↓
Need to construct a String?
      → StringBuilder
      ↓
Need frequency?
      → int[26] / HashMap
      ↓
Need existence?
      → HashSet
      ↓
Need index?
      → HashMap
      ↓
Need a pair?
      → Complement + HashMap
      ↓
Need same character counts?
      → Anagram pattern
      ↓
Need longest valid substring?
      → Hashing + Sliding Window
      ↓
Check constraints
      ↓
Code
      ↓
Dry run
      ↓
Edge cases
      ↓
Complexity
```

---

# 109. 🔗 NAVIGATION

⬅️ [Day 4 — Prefix Sum + Subarrays + Kadane](Day-04-Prefix-Sum-Subarrays-Kadane.md)

➡️ [Day 6 — Two Pointers + Sliding Window](Day-06-Two-Pointers-Sliding-Window.md)

---

# 🎯 FINAL DAY 5 MINDSET

The biggest shift today is from:

```text
"Search through everything again"
```

to:

```text
"Store useful information as I go."
```

That is the heart of hashing.

For example:

```text
Brute Force
    ↓
Search again
    ↓
O(n²)

Hashing
    ↓
Remember what I have seen
    ↓
Average O(1) lookup
    ↓
O(n)
```

And for strings:

```text
Need counts?
    ↓
Frequency

Need existence?
    ↓
Set

Need associated information?
    ↓
Map

Need a target pair?
    ↓
Complement

Need a valid substring?
    ↓
Hashing + Sliding Window
```

> **The goal is not to memorize HashMap syntax. The goal is to recognize what information the problem wants you to remember.**

**End of Day 5**
