# Day 9 --- Linked List + Stack + Queue

> Placement-focused Java DSA course \| Beginner + Revision

Today you will learn linked lists, fast/slow pointers, dummy nodes,
reversal, cycles, stacks, queues, deques, circular queues, and monotonic
stacks.

**Goal:** recognize the pattern first, then code it cleanly with correct
complexity and edge cases.

# 1. Today's Goal

By the end of Day 9 you should be able to: - create and traverse a
singly linked list; - insert and delete nodes; - reverse a list
in-place; - find the middle with fast/slow pointers; - detect a cycle
with Floyd's algorithm; - merge sorted lists; - use dummy nodes; -
understand doubly linked lists; - use `ArrayDeque` as a stack, queue,
and deque; - solve Valid Parentheses; - recognize monotonic-stack
problems; - explain time and space complexity.

**Priority:** Reverse Linked List, Fast/Slow, Cycle Detection, Merge Two
Sorted Lists, Stack, Valid Parentheses, Monotonic Stack, Queue.

# 2. Prerequisites + Navigation

Prerequisites: Java basics, arrays, strings, hashing, two pointers,
recursion.

Previous: - [Day 1 --- Java Basics](Day-01-Java-Basics.md) - [Day 2 ---
Number Problems + Patterns](Day-02-Number-Problems-Patterns.md) - [Day 3
--- Arrays Fundamentals](Day-03-Arrays-Fundamentals.md) - [Day 4 ---
Prefix Sum + Subarrays +
Kadane](Day-04-Prefix-Sum-Subarrays-Kadane.md) - [Day 5 --- Strings +
Hashing](Day-05-Strings-Hashing.md) - [Day 6 --- Two Pointers + Sliding
Window](Day-06-Two-Pointers-Sliding-Window.md) - [Day 7 --- Sorting +
Binary Search](Day-07-Sorting-Binary-Search.md) - [Day 8 --- Recursion +
Backtracking](Day-08-Recursion-Backtracking.md)

Next: [Day 10 --- Heap + Greedy +
Intervals](Day-10-Heap-Greedy-Intervals.md)

# 3. The Big Picture

``` text
LINKED LIST
head -> [10|next] -> [20|next] -> [30|null]

STACK
top
 ↓
[30]
[20]
[10]
LIFO

QUEUE
front                         rear
 ↓                              ↓
[10] -> [20] -> [30] -> [40]
FIFO
```

Remember: - Linked List = nodes connected by references - Stack = Last
In, First Out - Queue = First In, First Out - Deque = insert/remove at
both ends

# 4. Linked List --- Beginner Explanation

A linked list is a sequence of nodes. Each singly linked-list node
stores a value and a reference to the next node.

``` text
[value | next] -> [value | next] -> [value | null]
```

Unlike an array, a linked list does not support O(1) indexing. To reach
index `k`, you normally walk from the head.

Why use it? - insertion/deletion can be efficient when the relevant
location is known; - nodes do not need to be shifted like array
elements.

Trade-off: - Array: fast indexing, potentially expensive middle
insertion. - Linked list: sequential access, pointer-based
insertion/deletion.

**30-second revision:** access/search = O(n); head insertion/deletion =
O(1).

# 5. Node Implementation

``` java
class Node {
    int data;
    Node next;

    Node(int data) {
        this.data = data;
        this.next = null;
    }
}
```

Create:

``` java
Node a = new Node(10);
Node b = new Node(20);
Node c = new Node(30);

a.next = b;
b.next = c;

Node head = a;
```

Visualization:

``` text
head
 ↓
10 -> 20 -> 30 -> null
```

Terminology: - `head`: first node - `tail`: last node - `next`:
reference to next node - `null`: no next node

# 6. Traversal, Length, Search

### Traversal

``` java
void printList(Node head) {
    Node current = head;

    while (current != null) {
        System.out.print(current.data + " ");
        current = current.next;
    }
}
```

### Length

``` java
int length(Node head) {
    int count = 0;

    while (head != null) {
        count++;
        head = head.next;
    }

    return count;
}
```

### Search

``` java
boolean search(Node head, int target) {
    Node current = head;

    while (current != null) {
        if (current.data == target) return true;
        current = current.next;
    }

    return false;
}
```

All three are: - Time: O(n) - Extra space: O(1)

**Beginner mistake:** forgetting `current = current.next` creates an
infinite loop.

# 7. Insertion

### Insert at Head

For `10 -> 20 -> 30`, insert `5`:

``` text
5 -> 10 -> 20 -> 30
```

``` java
Node insertAtHead(Node head, int value) {
    Node node = new Node(value);
    node.next = head;
    return node;
}
```

Time: O(1), space: O(1).

### Insert at Tail

``` java
Node insertAtTail(Node head, int value) {
    Node node = new Node(value);

    if (head == null) return node;

    Node current = head;
    while (current.next != null) {
        current = current.next;
    }

    current.next = node;
    return head;
}
```

Without a maintained tail pointer: O(n).

### Insert at Index

``` java
Node insertAtIndex(Node head, int index, int value) {
    if (index == 0) {
        return insertAtHead(head, value);
    }

    Node current = head;

    for (int i = 0; i < index - 1 && current != null; i++) {
        current = current.next;
    }

    if (current == null) return head;

    Node node = new Node(value);
    node.next = current.next;
    current.next = node;

    return head;
}
```

Pattern: find the node **before** the insertion position.

# 8. Deletion

### Delete Head

``` java
Node deleteHead(Node head) {
    if (head == null) return null;
    return head.next;
}
```

O(1).

### Delete First Occurrence of a Value

``` java
Node deleteValue(Node head, int target) {
    if (head == null) return null;

    if (head.data == target) {
        return head.next;
    }

    Node current = head;

    while (current.next != null) {
        if (current.next.data == target) {
            current.next = current.next.next;
            return head;
        }
        current = current.next;
    }

    return head;
}
```

Why inspect `current.next`? Because then `current` is the previous node
and can bypass the node being deleted.

Time: O(n), space: O(1).

Edge cases: - empty list; - target at head; - target absent; - duplicate
target; - target at tail.

# 9. Reverse Linked List --- ⭐ Must Know

Input:

``` text
1 -> 2 -> 3 -> 4 -> null
```

Output:

``` text
4 -> 3 -> 2 -> 1 -> null
```

Use three references:

``` text
prev
current
next
```

``` java
Node reverse(Node head) {
    Node prev = null;
    Node current = head;

    while (current != null) {
        Node next = current.next;
        current.next = prev;
        prev = current;
        current = next;
    }

    return prev;
}
```

### Why save `next` first?

If you do:

``` java
current.next = prev;
```

you destroy the old route to the next node. Saving it first prevents
losing the remaining list.

### Dry run

``` text
start:
prev = null
current = 1

iteration 1:
next = 2
1 -> null
prev = 1
current = 2

iteration 2:
2 -> 1 -> null

iteration 3:
3 -> 2 -> 1 -> null

iteration 4:
4 -> 3 -> 2 -> 1 -> null
```

Complexity: O(n) time, O(1) extra space.

### Brute force -\> optimal

Brute force can copy values into an array and rebuild: O(n) time, O(n)
space.

Optimal changes references in-place: O(n) time, O(1) space.

# 10. Recursive Reverse

``` java
Node reverseRecursive(Node head) {
    if (head == null || head.next == null) {
        return head;
    }

    Node newHead = reverseRecursive(head.next);

    head.next.next = head;
    head.next = null;

    return newHead;
}
```

Time: O(n).

Extra space: O(n) because of the recursion call stack.

For most placement implementations, the iterative version is the safest
O(1)-space template.

# 11. Fast + Slow Pointers

Use two references: - `slow` moves one step; - `fast` moves two steps.

Template:

``` java
Node slow = head;
Node fast = head;

while (fast != null && fast.next != null) {
    slow = slow.next;
    fast = fast.next.next;
}
```

Think fast/slow when the problem mentions: - middle of a linked list; -
cycle/loop; - cycle entry; - palindrome linked list; - two-speed
traversal; - nth node from the end (often paired with a fixed gap).

# 12. Middle of Linked List

For:

``` text
1 -> 2 -> 3 -> 4 -> 5
```

middle is `3`.

For an even list, the standard LeetCode problem returns the second
middle. citeturn0search2

Optimal:

``` java
Node middleNode(Node head) {
    Node slow = head;
    Node fast = head;

    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
    }

    return slow;
}
```

Brute force: count length, then walk to `length/2`. Still O(n), but
requires two passes.

Optimal: one pass, O(n) time and O(1) space.

# 13. Cycle Detection --- Floyd

A cycle means some node eventually points back to an earlier node:

``` text
1 -> 2 -> 3 -> 4
          ^    |
          |____|
```

### Brute force

Use `HashSet<Node>` to remember visited references.

Time O(n), space O(n).

### Optimal

``` java
boolean hasCycle(Node head) {
    Node slow = head;
    Node fast = head;

    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;

        if (slow == fast) {
            return true;
        }
    }

    return false;
}
```

Why it works: inside a cycle, the fast pointer gains one node per
iteration and eventually catches the slow pointer.

Time O(n), space O(1).

**Important:** compare references with `slow == fast`, not values. Two
different nodes may contain the same value.

# 14. Cycle Entry

After Floyd detects a meeting point, reset one pointer to `head`. Move
both one step at a time. Their next meeting point is the cycle entry.

``` java
Node cycleStart(Node head) {
    Node slow = head;
    Node fast = head;

    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;

        if (slow == fast) break;
    }

    if (fast == null || fast.next == null) return null;

    slow = head;

    while (slow != fast) {
        slow = slow.next;
        fast = fast.next;
    }

    return slow;
}
```

Time O(n), space O(1).

# 15. Dummy Node Pattern

A dummy node is a sentinel before the real head.

``` text
dummy -> actual list
```

It reduces special cases when: - head may be deleted; - head may
change; - building a result list; - merging lists.

Template:

``` java
Node dummy = new Node(0);
Node current = dummy;

// attach nodes using current.next

return dummy.next;
```

Remember: the dummy itself is not part of the answer.

# 16. Merge Two Sorted Linked Lists

Input:

``` text
1 -> 3 -> 5
2 -> 4 -> 6
```

Output:

``` text
1 -> 2 -> 3 -> 4 -> 5 -> 6
```

The official LeetCode problem asks for one sorted list formed by
splicing the two sorted lists. citeturn0search0

``` java
Node mergeTwoLists(Node a, Node b) {
    Node dummy = new Node(0);
    Node current = dummy;

    while (a != null && b != null) {
        if (a.data <= b.data) {
            current.next = a;
            a = a.next;
        } else {
            current.next = b;
            b = b.next;
        }

        current = current.next;
    }

    current.next = (a != null) ? a : b;
    return dummy.next;
}
```

Time O(n+m), extra space O(1).

Pattern: **two pointers + dummy node**.

# 17. Intersection of Two Linked Lists

Intersection means the two lists share the same actual node, not merely
equal values.

Pointer switching:

``` java
Node getIntersection(Node headA, Node headB) {
    Node a = headA;
    Node b = headB;

    while (a != b) {
        a = (a == null) ? headB : a.next;
        b = (b == null) ? headA : b.next;
    }

    return a;
}
```

Each pointer traverses A+B, balancing different prefix lengths.

Time O(n+m), space O(1).

**Clue:** two lists + same node/reference -\> pointer switching.

# 18. Remove Nth Node From End

Example:

``` text
1 -> 2 -> 3 -> 4 -> 5
n = 2
```

Result:

``` text
1 -> 2 -> 3 -> 5
```

Use a dummy and keep a gap of `n` between two pointers.

``` java
Node removeNthFromEnd(Node head, int n) {
    Node dummy = new Node(0);
    dummy.next = head;

    Node fast = dummy;
    Node slow = dummy;

    for (int i = 0; i < n; i++) {
        fast = fast.next;
    }

    while (fast.next != null) {
        fast = fast.next;
        slow = slow.next;
    }

    slow.next = slow.next.next;
    return dummy.next;
}
```

Time O(n), space O(1).

# 19. Doubly Linked List

A doubly linked-list node has:

``` text
prev <- [data] -> next
```

``` java
class DNode {
    int data;
    DNode prev;
    DNode next;

    DNode(int data) {
        this.data = data;
    }
}
```

Visualization:

``` text
null <- 10 <-> 20 <-> 30 -> null
```

Advantages: - forward and backward traversal; - easier deletion when a
node reference is available.

Cost: - extra `prev` reference; - more pointer updates and more
opportunities for bugs.

Comparison:

  Feature       Singly   Doubly
  ------------- -------- --------
  next          yes      yes
  prev          no       yes
  forward       yes      yes
  backward      no       yes
  memory/node   lower    higher

# 20. Circular Linked List

In a circular list, the final node points back to the first node:

``` text
10 -> 20 -> 30
^           |
|___________|
```

There is no `null` at the end.

Useful in some round-robin and cyclic processing problems. For
placements, master singly lists and fast/slow cycle detection before
spending time on advanced circular-list implementations.

# 21. Stack --- Beginner Explanation

A stack follows **LIFO: Last In, First Out**.

Think of plates:

``` text
push 10
push 20
push 30

top
 ↓
30
20
10
```

`pop()` removes 30.

Operations: - `push(x)` --- add - `pop()` --- remove top - `peek()` ---
inspect top - `isEmpty()` --- check empty

Typical complexity: O(1) for push, pop, peek.

# 22. Java Stack with ArrayDeque

For normal coding-interview stack usage, use:

``` java
Deque<Integer> stack = new ArrayDeque<>();

stack.push(10);
stack.push(20);

int top = stack.peek();
int removed = stack.pop();
```

`ArrayDeque` is also useful as a deque and queue.

Avoid confusing: - `push/pop` = stack semantics; - `offer/poll` = queue
semantics.

# 23. Valid Parentheses

Clues: - matching brackets; - nesting; - most recent unmatched opening
bracket.

These are LIFO clues, so use a stack.

The standard problem checks that opening brackets are closed by the same
type and in the correct order. citeturn0search10

``` java
boolean isValid(String s) {
    Deque<Character> stack = new ArrayDeque<>();

    for (char ch : s.toCharArray()) {
        if (ch == '(' || ch == '[' || ch == '{') {
            stack.push(ch);
        } else {
            if (stack.isEmpty()) return false;

            char top = stack.pop();

            if ((ch == ')' && top != '(') ||
                (ch == ']' && top != '[') ||
                (ch == '}' && top != '{')) {
                return false;
            }
        }
    }

    return stack.isEmpty();
}
```

Example:

``` text
([{}])
push (, [, {
) -> top (
] -> top [
} -> top {
empty -> valid
```

Time O(n), space O(n).

# 24. Min Stack

A Min Stack supports normal stack operations plus `getMin()` in O(1).

Use two stacks: - normal values; - current minimums.

``` java
class MinStack {
    Deque<Integer> stack = new ArrayDeque<>();
    Deque<Integer> mins = new ArrayDeque<>();

    void push(int x) {
        stack.push(x);

        if (mins.isEmpty() || x <= mins.peek()) {
            mins.push(x);
        }
    }

    void pop() {
        int x = stack.pop();

        if (x == mins.peek()) {
            mins.pop();
        }
    }

    int top() {
        return stack.peek();
    }

    int getMin() {
        return mins.peek();
    }
}
```

All four operations are O(1). Extra space O(n).

# 25. Monotonic Stack

A monotonic stack keeps values or indices in increasing/decreasing
order.

Common clues: - next greater element; - next smaller element; - previous
greater/smaller; - nearest greater/smaller; - daily temperatures.

Brute force often scans right for every index: O(n²).

Monotonic stack often reduces this to O(n) because each index is pushed
once and popped once.

Generic form:

``` java
Deque<Integer> stack = new ArrayDeque<>();

for (int i = 0; i < n; i++) {
    while (!stack.isEmpty() && condition(nums[i], nums[stack.peek()])) {
        int index = stack.pop();
        // resolve index
    }
    stack.push(i);
}
```

# 26. Next Greater Element

Example:

``` text
[2, 1, 5, 3]
```

Output:

``` text
[5, 5, -1, -1]
```

Optimal:

``` java
int[] nextGreater(int[] nums) {
    int n = nums.length;
    int[] ans = new int[n];
    Arrays.fill(ans, -1);

    Deque<Integer> stack = new ArrayDeque<>();

    for (int i = 0; i < n; i++) {
        while (!stack.isEmpty() && nums[i] > nums[stack.peek()]) {
            int index = stack.pop();
            ans[index] = nums[i];
        }
        stack.push(i);
    }

    return ans;
}
```

Time O(n), space O(n).

Why O(n)? Each index enters the stack once and leaves at most once.

# 27. Daily Temperatures

Input:

``` text
[73,74,75,71,69,72,76,73]
```

Output:

``` text
[1,1,4,2,1,1,0,0]
```

Use a decreasing monotonic stack of indices.

``` java
int[] dailyTemperatures(int[] temperatures) {
    int n = temperatures.length;
    int[] answer = new int[n];
    Deque<Integer> stack = new ArrayDeque<>();

    for (int i = 0; i < n; i++) {
        while (!stack.isEmpty()
                && temperatures[i] > temperatures[stack.peek()]) {

            int previous = stack.pop();
            answer[previous] = i - previous;
        }

        stack.push(i);
    }

    return answer;
}
```

Time O(n), space O(n).

# 28. Queue --- Beginner Explanation

A queue follows **FIFO: First In, First Out**.

``` text
front                    rear
 ↓                         ↓
10 -> 20 -> 30 -> 40
```

Operations: - `offer` = add at rear; - `poll` = remove from front; -
`peek` = inspect front.

Java:

``` java
Deque<Integer> queue = new ArrayDeque<>();

queue.offer(10);
queue.offer(20);
queue.offer(30);

int front = queue.peek();
int removed = queue.poll();
```

Typical operation complexity: O(1).

# 29. Queue vs Stack vs Deque

  Structure   Rule        Java operations
  ----------- ----------- ---------------------------------
  Stack       LIFO        push, pop, peek
  Queue       FIFO        offer, poll, peek
  Deque       both ends   offerFirst/Last, pollFirst/Last

A deque can implement both stack and queue behavior.

# 30. Queue and BFS

Queues are central to BFS and tree level-order traversal.

Example:

``` text
       1
      /      2   3
    /    4   5
```

BFS:

``` text
1 2 3 4 5
```

Queue process:

``` text
[1]
poll 1 -> add 2,3
[2,3]
poll 2 -> add 4,5
[3,4,5]
...
```

**Pattern clue:** "level by level", "minimum steps in an unweighted
graph", or "BFS" -\> think queue.

# 31. Deque

Deque = Double Ended Queue.

``` java
Deque<Integer> deque = new ArrayDeque<>();

deque.offerFirst(10);
deque.offerLast(20);

deque.pollFirst();
deque.pollLast();
```

Both ends are available.

This structure becomes especially useful later in sliding-window maximum
and other two-ended processing patterns.

# 32. Circular Queue

A fixed-size queue can reuse freed positions with wrap-around.

Formula:

``` java
next = (index + 1) % capacity;
```

Example:

``` text
capacity = 5
index = 4
next = (4 + 1) % 5 = 0
```

Simple implementation:

``` java
class CircularQueue {
    int[] arr;
    int front = 0;
    int rear = 0;
    int size = 0;

    CircularQueue(int capacity) {
        arr = new int[capacity];
    }

    boolean isEmpty() {
        return size == 0;
    }

    boolean isFull() {
        return size == arr.length;
    }

    void offer(int x) {
        if (isFull()) return;
        arr[rear] = x;
        rear = (rear + 1) % arr.length;
        size++;
    }

    int poll() {
        if (isEmpty()) return -1;
        int x = arr[front];
        front = (front + 1) % arr.length;
        size--;
        return x;
    }

    int peek() {
        return isEmpty() ? -1 : arr[front];
    }
}
```

Operations are O(1).

# 33. Java-Specific DSA Notes

-   Prefer `ArrayDeque` for ordinary stack/queue operations.
-   `LinkedList` can implement `List`, `Queue`, and `Deque`, but
    explicit linked-list questions usually require your own `Node`.
-   In linked-list reversal, save `next` before changing `current.next`.
-   When node identity matters, compare references with `==`.
-   Always guard `fast != null && fast.next != null`.
-   Return the new head after reversal.
-   Use a dummy node when head changes are making the code complicated.
-   For `ArrayDeque`, do not insert `null`.

# 34. Complexity Cheat Sheet

  Problem/Operation                      Time   Extra Space
  ---------------------------------- -------- -------------
  linked-list traversal                  O(n)          O(1)
  search                                 O(n)          O(1)
  access by index                        O(n)          O(1)
  insert head                            O(1)          O(1)
  delete head                            O(1)          O(1)
  insert tail without tail pointer       O(n)          O(1)
  reverse list                           O(n)          O(1)
  recursive reverse                      O(n)    O(n) stack
  middle                                 O(n)          O(1)
  cycle detection                        O(n)          O(1)
  merge two sorted lists               O(n+m)          O(1)
  intersection                         O(n+m)          O(1)
  stack push/pop/peek                    O(1)   O(1) per op
  queue offer/poll/peek                  O(1)   O(1) per op
  monotonic stack                        O(n)          O(n)

# 35. Brute Force → Optimal Map

  Problem              Brute Force            Optimal
  -------------------- ---------------------- --------------------
  Reverse LL           array copy             three pointers
  Middle               length + second pass   fast/slow
  Cycle                HashSet                Floyd
  Merge lists          collect + sort         two pointers
  Intersection         HashSet                pointer switching
  Nth from end         length + pass          fixed-gap pointers
  Valid parentheses    repeated matching      stack
  Next greater         nested loops           monotonic stack
  Daily temperatures   nested loops           monotonic stack

# 36. Pattern Recognition

### Reverse

Clues: reverse, in-place linked-list links. Think: `prev/current/next`.

### Fast/Slow

Clues: middle, cycle, loop, two speeds. Think: one pointer +1, one +2.

### Dummy Node

Clues: head can change, deletion/insertion near head, build result list.
Think: sentinel before real head.

### Stack

Clues: nested, matching, most recent unmatched, undo. Think: LIFO.

### Monotonic Stack

Clues: next/previous greater or smaller, nearest greater/smaller. Think:
ordered stack of unresolved indices.

### Queue

Clues: first come first served, BFS, level order. Think: FIFO.

### Circular Queue

Clues: fixed capacity + reuse freed positions. Think: modulo.

# 37. Edge Cases

Linked list: - empty list; - one node; - two nodes; - delete head; -
delete tail; - target absent; - duplicate values; - even/odd length; -
cycle.

Stack: - empty; - one item; - closing bracket first; - mismatched
bracket; - all opening brackets; - duplicate minimum values.

Queue: - empty; - one item; - full; - wrap-around; - repeated
offer/poll.

Always ask: "What happens when the input is empty?"

# 38. Mini Practice

## Problem 1 --- Count Nodes

Input list:

``` text
5 -> 8 -> 2 -> 9
```

Expected: `4`.

Hint: traverse until `null`.

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
int countNodes(Node head) {
    int count = 0;

    while (head != null) {
        count++;
        head = head.next;
    }

    return count;
}
```

O(n) time, O(1) space.
```{=html}
</details>
```
## Problem 2 --- Reverse

Input:

``` text
1 -> 2 -> 3
```

Expected:

``` text
3 -> 2 -> 1
```

Hint: `prev`, `current`, `next`.

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
Node reverse(Node head) {
    Node prev = null;
    Node current = head;

    while (current != null) {
        Node next = current.next;
        current.next = prev;
        prev = current;
        current = next;
    }

    return prev;
}
```

```{=html}
</details>
```
# 39. Full Worked Example --- Reverse

**Input:** `1 -> 2 -> 3 -> 4`

**Observation:** each link points in the wrong direction.

**Approach:** reverse one link per iteration.

**Algorithm:** 1. Save next. 2. Point current backward. 3. Move
previous. 4. Move current. 5. Return previous.

**Code:**

``` java
Node reverseList(Node head) {
    Node prev = null;
    Node current = head;

    while (current != null) {
        Node next = current.next;
        current.next = prev;
        prev = current;
        current = next;
    }

    return prev;
}
```

**Output:** `4 -> 3 -> 2 -> 1`

**Complexity:** O(n) time, O(1) space.

**Edge cases:** null and one-node list return safely.

# 40. Full Worked Example --- Middle

**Input:** `1 -> 2 -> 3 -> 4 -> 5`

**Observation:** fast travels twice as quickly.

**Code:**

``` java
Node middleNode(Node head) {
    Node slow = head;
    Node fast = head;

    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
    }

    return slow;
}
```

**Output:** node `3`.

Time O(n), space O(1).

# 41. Full Worked Example --- Cycle

**Input:** `1 -> 2 -> 3 -> 4 -> 2 ...`

**Observation:** a cycle means fast and slow eventually meet.

``` java
boolean hasCycle(Node head) {
    Node slow = head;
    Node fast = head;

    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;

        if (slow == fast) return true;
    }

    return false;
}
```

Output: `true`.

Time O(n), space O(1).

# 42. Full Worked Example --- Valid Parentheses

**Input:** `"{[()]}"`

**Observation:** the latest opening bracket must close first.

**Approach:** push opens; each close must match stack top.

``` java
boolean isValid(String s) {
    Deque<Character> stack = new ArrayDeque<>();

    for (char ch : s.toCharArray()) {
        if (ch == '(' || ch == '[' || ch == '{') {
            stack.push(ch);
        } else {
            if (stack.isEmpty()) return false;

            char top = stack.pop();

            if ((ch == ')' && top != '(') ||
                (ch == ']' && top != '[') ||
                (ch == '}' && top != '{')) {
                return false;
            }
        }
    }

    return stack.isEmpty();
}
```

Output: `true`.

Time O(n), space O(n).

# 43. Full Worked Example --- Next Greater

**Input:** `[2,1,5,3]`

**Brute force:** for every element, scan right -\> O(n²).

**Observation:** unresolved indices can wait on a monotonic stack.

``` java
int[] nextGreater(int[] nums) {
    int[] ans = new int[nums.length];
    Arrays.fill(ans, -1);

    Deque<Integer> stack = new ArrayDeque<>();

    for (int i = 0; i < nums.length; i++) {
        while (!stack.isEmpty() && nums[i] > nums[stack.peek()]) {
            ans[stack.pop()] = nums[i];
        }
        stack.push(i);
    }

    return ans;
}
```

Output: `[5,5,-1,-1]`.

Time O(n), space O(n).

# 44. Interview Explanations

### Linked List

"A linked list is a sequence of nodes where each node stores data and a
reference to the next node. It has O(n) access but can support O(1) head
insertion/deletion."

### Reverse

"I save the next node, reverse the current link, then move previous and
current. This gives O(n) time and O(1) space."

### Fast/Slow

"Slow moves one step and fast two. This finds the middle in one pass and
supports Floyd cycle detection."

### Stack

"A stack is LIFO. It is natural for nested structures, matching
brackets, undo-like behavior, and monotonic-stack problems."

### Queue

"A queue is FIFO. It is fundamental for BFS and level-order traversal."

# 45. Constraint Thinking

If `n` is around `10^5`, avoid O(n²) unless constraints clearly permit
it.

For linked lists: - avoid repeatedly traversing from head; - use
fast/slow or two pointers; - use O(1) pointer manipulation when
possible.

For next-greater problems: - O(n²) nested scanning is usually the
bottleneck; - monotonic stack can reduce it to O(n).

# 46. Practice Problems --- Verified URLs

### Easy

1.  Reverse Linked List --- pointer reversal\
    https://leetcode.com/problems/reverse-linked-list/

2.  Middle of the Linked List --- fast/slow\
    https://leetcode.com/problems/middle-of-the-linked-list/

3.  Linked List Cycle --- Floyd\
    https://leetcode.com/problems/linked-list-cycle/

4.  Merge Two Sorted Lists --- merge pointers\
    https://leetcode.com/problems/merge-two-sorted-lists/

5.  Intersection of Two Linked Lists --- pointer switching\
    https://leetcode.com/problems/intersection-of-two-linked-lists/

6.  Valid Parentheses --- stack\
    https://leetcode.com/problems/valid-parentheses/

### Medium

7.  Remove Nth Node From End of List --- two pointers + dummy\
    https://leetcode.com/problems/remove-nth-node-from-end-of-list/

8.  Min Stack --- auxiliary stack\
    https://leetcode.com/problems/min-stack/

9.  Daily Temperatures --- monotonic stack\
    https://leetcode.com/problems/daily-temperatures/

10. Design Circular Queue --- circular array\
    https://leetcode.com/problems/design-circular-queue/

11. Linked List Cycle II --- cycle entry\
    https://leetcode.com/problems/linked-list-cycle-ii/

12. Reorder List --- middle + reverse + merge\
    https://leetcode.com/problems/reorder-list/

### Advanced

13. Merge k Sorted Lists --- heap + lists\
    https://leetcode.com/problems/merge-k-sorted-lists/

14. Reverse Nodes in k-Group --- grouped reversal\
    https://leetcode.com/problems/reverse-nodes-in-k-group/

# 47. Recommended Practice Order

**Round 1 --- Must Do** 1. Reverse Linked List 2. Middle of Linked List
3. Linked List Cycle 4. Merge Two Sorted Lists 5. Valid Parentheses

**Round 2** 6. Intersection of Two Linked Lists 7. Remove Nth Node From
End 8. Min Stack 9. Daily Temperatures

**Round 3** 10. Linked List Cycle II 11. Design Circular Queue 12.
Reorder List

**Round 4 --- Advanced** 13. Merge k Sorted Lists 14. Reverse Nodes in
k-Group

# 48. Daily Test --- 10 Questions

1.  A singly linked-list node normally contains: A. value only B.
    value + next C. index + value D. previous only

2.  Linked-list random access is usually: A. O(1) B. O(log n) C. O(n) D.
    O(n log n)

3.  Which pattern finds the middle in one pass? A. binary search B.
    prefix sum C. fast/slow D. HashMap

4.  Floyd's algorithm is used for: A. sorting B. cycle detection C.
    hashing D. binary search

5.  A stack follows: A. FIFO B. LIFO C. random D. sorted

6.  A queue follows: A. FIFO B. LIFO C. DFS D. binary order

7.  Convenient Java stack/deque implementation: A. ArrayDeque B.
    String C. HashMap D. TreeSet

8.  Next greater element commonly uses: A. prefix sum B. monotonic
    stack C. binary search D. union-find

9.  Iterative reversal commonly uses: A. one pointer B.
    previous/current/next C. two arrays D. HashMap

10. Exact same linked-list node should be compared using: A. value B.
    index C. reference identity D. string

# 49. Answer Key

``` text
1 -> B
2 -> C
3 -> C
4 -> B
5 -> B
6 -> A
7 -> A
8 -> B
9 -> B
10 -> C
```

Score guide: - 9--10: excellent - 7--8: revise weak patterns - 5--6:
revisit core templates - 0--4: restudy before moving on

# 50. Pattern Recognition Test

Identify the pattern:

1.  "Find the node where a linked-list loop begins." -\> Floyd /
    fast-slow.
2.  "Find the middle in one traversal." -\> fast/slow.
3.  "Check nested brackets." -\> stack.
4.  "Find the next warmer day." -\> monotonic stack.
5.  "Process a tree level by level." -\> queue/BFS.
6.  "Reverse links in-place." -\> prev/current/next.
7.  "Merge two sorted linked lists." -\> two pointers + dummy.
8.  "Remove nth from end in one pass." -\> two pointers + gap.

# 51. Templates to Memorize

### Traverse

``` java
Node current = head;
while (current != null) {
    // process
    current = current.next;
}
```

### Reverse

``` java
Node prev = null;
Node current = head;

while (current != null) {
    Node next = current.next;
    current.next = prev;
    prev = current;
    current = next;
}

return prev;
```

### Fast/Slow

``` java
Node slow = head;
Node fast = head;

while (fast != null && fast.next != null) {
    slow = slow.next;
    fast = fast.next.next;
}
```

### Cycle

``` java
while (fast != null && fast.next != null) {
    slow = slow.next;
    fast = fast.next.next;
    if (slow == fast) return true;
}
return false;
```

### Stack

``` java
Deque<Integer> stack = new ArrayDeque<>();
stack.push(x);
stack.peek();
stack.pop();
```

### Queue

``` java
Deque<Integer> queue = new ArrayDeque<>();
queue.offer(x);
queue.peek();
queue.poll();
```

### Monotonic Stack

``` java
Deque<Integer> stack = new ArrayDeque<>();

for (int i = 0; i < n; i++) {
    while (!stack.isEmpty() && condition(nums[i], nums[stack.peek()])) {
        int index = stack.pop();
        // resolve
    }
    stack.push(i);
}
```

# 52. 30-Second Revision

``` text
Node = data + next

Reverse:
prev/current/next

Middle:
slow +1, fast +2

Cycle:
slow == fast

Dummy:
dummy.next = real answer

Stack:
LIFO

Queue:
FIFO

Deque:
both ends

Monotonic stack:
next/previous greater or smaller

Circular queue:
(index + 1) % capacity
```

# 53. Homework

### Mandatory

-   Reverse Linked List
-   Middle of Linked List
-   Linked List Cycle
-   Merge Two Sorted Lists
-   Valid Parentheses
-   Remove Nth Node From End
-   Min Stack
-   Daily Temperatures

### Optional

-   Intersection of Two Linked Lists
-   Linked List Cycle II
-   Reorder List
-   Design Circular Queue

### Advanced

-   Merge k Sorted Lists
-   Reverse Nodes in k-Group

# 54. Completion Checklist

-   [ ] I understand node/reference structure.
-   [ ] I can traverse a linked list.
-   [ ] I can insert at head and tail.
-   [ ] I can delete a node.
-   [ ] I can reverse a list iteratively.
-   [ ] I understand recursive reversal.
-   [ ] I can find the middle.
-   [ ] I can detect a cycle.
-   [ ] I understand cycle entry.
-   [ ] I understand dummy nodes.
-   [ ] I can merge sorted lists.
-   [ ] I understand doubly linked lists.
-   [ ] I can use ArrayDeque as a stack.
-   [ ] I can solve Valid Parentheses.
-   [ ] I understand Min Stack.
-   [ ] I recognize monotonic-stack clues.
-   [ ] I can use ArrayDeque as a queue.
-   [ ] I understand circular queues.
-   [ ] I know the complexity of the major patterns.
-   [ ] I completed the daily test.
-   [ ] I completed the mandatory practice.

# 55. Final Mental Map

``` text
                 DAY 9
                   |
        +----------+----------+
        |                     |
   LINKED LIST           STACK / QUEUE
        |                     |
   +----+----+          +-----+-----+
   |    |    |          |     |     |
Reverse Fast Dummy     Stack Queue Deque
   |    |    |          |     |     |
 prev  slow result     LIFO  FIFO both ends
 curr  fast  head       |     |
 next                  matching BFS
   |                     |
 cycle                monotonic
 merge
```

The core mental model:

``` text
Linked List -> pointer manipulation
Fast/Slow   -> middle/cycle
Dummy Node  -> simplify head/result handling
Stack       -> LIFO/nesting
Queue       -> FIFO/BFS
Monotonic   -> next greater/smaller
```

# 56. Day 9 Completion Standard

Do not move forward merely because you read the notes.

Before Day 10, you should be able to code without copying:

1.  Reverse Linked List
2.  Middle of Linked List
3.  Linked List Cycle
4.  Merge Two Sorted Lists
5.  Valid Parentheses

For each one, explain: - why the pattern works; - brute force and its
bottleneck; - optimized approach; - time complexity; - space
complexity; - edge cases.

**Previous:** [Day 8 --- Recursion +
Backtracking](Day-08-Recursion-Backtracking.md)

**Next:** [Day 10 --- Heap + Greedy +
Intervals](Day-10-Heap-Greedy-Intervals.md)

# Revision Drill 1

### Recall

Without looking at the earlier sections, answer these mentally:

1.  What are the three pointers used in iterative reversal?
2.  What does `fast` do compared with `slow`?
3.  Why is `slow == fast` used for cycle detection?
4.  When is a dummy node useful?
5.  Why is `ArrayDeque` useful for stack and queue problems?
6.  What does LIFO mean?
7.  What does FIFO mean?
8.  What clues suggest a monotonic stack?
9.  Why is a queue natural for BFS?
10. What is the complexity of the standard O(n) linked-list templates?

**Coding prompt:** write one template from memory, then compare it with
the template section.

# Revision Drill 2

### Recall

Without looking at the earlier sections, answer these mentally:

1.  What are the three pointers used in iterative reversal?
2.  What does `fast` do compared with `slow`?
3.  Why is `slow == fast` used for cycle detection?
4.  When is a dummy node useful?
5.  Why is `ArrayDeque` useful for stack and queue problems?
6.  What does LIFO mean?
7.  What does FIFO mean?
8.  What clues suggest a monotonic stack?
9.  Why is a queue natural for BFS?
10. What is the complexity of the standard O(n) linked-list templates?

**Coding prompt:** write one template from memory, then compare it with
the template section.

# Revision Drill 3

### Recall

Without looking at the earlier sections, answer these mentally:

1.  What are the three pointers used in iterative reversal?
2.  What does `fast` do compared with `slow`?
3.  Why is `slow == fast` used for cycle detection?
4.  When is a dummy node useful?
5.  Why is `ArrayDeque` useful for stack and queue problems?
6.  What does LIFO mean?
7.  What does FIFO mean?
8.  What clues suggest a monotonic stack?
9.  Why is a queue natural for BFS?
10. What is the complexity of the standard O(n) linked-list templates?

**Coding prompt:** write one template from memory, then compare it with
the template section.

# Revision Drill 4

### Recall

Without looking at the earlier sections, answer these mentally:

1.  What are the three pointers used in iterative reversal?
2.  What does `fast` do compared with `slow`?
3.  Why is `slow == fast` used for cycle detection?
4.  When is a dummy node useful?
5.  Why is `ArrayDeque` useful for stack and queue problems?
6.  What does LIFO mean?
7.  What does FIFO mean?
8.  What clues suggest a monotonic stack?
9.  Why is a queue natural for BFS?
10. What is the complexity of the standard O(n) linked-list templates?

**Coding prompt:** write one template from memory, then compare it with
the template section.

# Revision Drill 5

### Recall

Without looking at the earlier sections, answer these mentally:

1.  What are the three pointers used in iterative reversal?
2.  What does `fast` do compared with `slow`?
3.  Why is `slow == fast` used for cycle detection?
4.  When is a dummy node useful?
5.  Why is `ArrayDeque` useful for stack and queue problems?
6.  What does LIFO mean?
7.  What does FIFO mean?
8.  What clues suggest a monotonic stack?
9.  Why is a queue natural for BFS?
10. What is the complexity of the standard O(n) linked-list templates?

**Coding prompt:** write one template from memory, then compare it with
the template section.

# Revision Drill 6

### Recall

Without looking at the earlier sections, answer these mentally:

1.  What are the three pointers used in iterative reversal?
2.  What does `fast` do compared with `slow`?
3.  Why is `slow == fast` used for cycle detection?
4.  When is a dummy node useful?
5.  Why is `ArrayDeque` useful for stack and queue problems?
6.  What does LIFO mean?
7.  What does FIFO mean?
8.  What clues suggest a monotonic stack?
9.  Why is a queue natural for BFS?
10. What is the complexity of the standard O(n) linked-list templates?

**Coding prompt:** write one template from memory, then compare it with
the template section.

# Revision Drill 7

### Recall

Without looking at the earlier sections, answer these mentally:

1.  What are the three pointers used in iterative reversal?
2.  What does `fast` do compared with `slow`?
3.  Why is `slow == fast` used for cycle detection?
4.  When is a dummy node useful?
5.  Why is `ArrayDeque` useful for stack and queue problems?
6.  What does LIFO mean?
7.  What does FIFO mean?
8.  What clues suggest a monotonic stack?
9.  Why is a queue natural for BFS?
10. What is the complexity of the standard O(n) linked-list templates?

**Coding prompt:** write one template from memory, then compare it with
the template section.

# Revision Drill 8

### Recall

Without looking at the earlier sections, answer these mentally:

1.  What are the three pointers used in iterative reversal?
2.  What does `fast` do compared with `slow`?
3.  Why is `slow == fast` used for cycle detection?
4.  When is a dummy node useful?
5.  Why is `ArrayDeque` useful for stack and queue problems?
6.  What does LIFO mean?
7.  What does FIFO mean?
8.  What clues suggest a monotonic stack?
9.  Why is a queue natural for BFS?
10. What is the complexity of the standard O(n) linked-list templates?

**Coding prompt:** write one template from memory, then compare it with
the template section.

# Revision Drill 9

### Recall

Without looking at the earlier sections, answer these mentally:

1.  What are the three pointers used in iterative reversal?
2.  What does `fast` do compared with `slow`?
3.  Why is `slow == fast` used for cycle detection?
4.  When is a dummy node useful?
5.  Why is `ArrayDeque` useful for stack and queue problems?
6.  What does LIFO mean?
7.  What does FIFO mean?
8.  What clues suggest a monotonic stack?
9.  Why is a queue natural for BFS?
10. What is the complexity of the standard O(n) linked-list templates?

**Coding prompt:** write one template from memory, then compare it with
the template section.

# Revision Drill 10

### Recall

Without looking at the earlier sections, answer these mentally:

1.  What are the three pointers used in iterative reversal?
2.  What does `fast` do compared with `slow`?
3.  Why is `slow == fast` used for cycle detection?
4.  When is a dummy node useful?
5.  Why is `ArrayDeque` useful for stack and queue problems?
6.  What does LIFO mean?
7.  What does FIFO mean?
8.  What clues suggest a monotonic stack?
9.  Why is a queue natural for BFS?
10. What is the complexity of the standard O(n) linked-list templates?

**Coding prompt:** write one template from memory, then compare it with
the template section.

# Revision Drill 11

### Recall

Without looking at the earlier sections, answer these mentally:

1.  What are the three pointers used in iterative reversal?
2.  What does `fast` do compared with `slow`?
3.  Why is `slow == fast` used for cycle detection?
4.  When is a dummy node useful?
5.  Why is `ArrayDeque` useful for stack and queue problems?
6.  What does LIFO mean?
7.  What does FIFO mean?
8.  What clues suggest a monotonic stack?
9.  Why is a queue natural for BFS?
10. What is the complexity of the standard O(n) linked-list templates?

**Coding prompt:** write one template from memory, then compare it with
the template section.

# Revision Drill 12

### Recall

Without looking at the earlier sections, answer these mentally:

1.  What are the three pointers used in iterative reversal?
2.  What does `fast` do compared with `slow`?
3.  Why is `slow == fast` used for cycle detection?
4.  When is a dummy node useful?
5.  Why is `ArrayDeque` useful for stack and queue problems?
6.  What does LIFO mean?
7.  What does FIFO mean?
8.  What clues suggest a monotonic stack?
9.  Why is a queue natural for BFS?
10. What is the complexity of the standard O(n) linked-list templates?

**Coding prompt:** write one template from memory, then compare it with
the template section.

# Revision Drill 13

### Recall

Without looking at the earlier sections, answer these mentally:

1.  What are the three pointers used in iterative reversal?
2.  What does `fast` do compared with `slow`?
3.  Why is `slow == fast` used for cycle detection?
4.  When is a dummy node useful?
5.  Why is `ArrayDeque` useful for stack and queue problems?
6.  What does LIFO mean?
7.  What does FIFO mean?
8.  What clues suggest a monotonic stack?
9.  Why is a queue natural for BFS?
10. What is the complexity of the standard O(n) linked-list templates?

**Coding prompt:** write one template from memory, then compare it with
the template section.

# Revision Drill 14

### Recall

Without looking at the earlier sections, answer these mentally:

1.  What are the three pointers used in iterative reversal?
2.  What does `fast` do compared with `slow`?
3.  Why is `slow == fast` used for cycle detection?
4.  When is a dummy node useful?
5.  Why is `ArrayDeque` useful for stack and queue problems?
6.  What does LIFO mean?
7.  What does FIFO mean?
8.  What clues suggest a monotonic stack?
9.  Why is a queue natural for BFS?
10. What is the complexity of the standard O(n) linked-list templates?

**Coding prompt:** write one template from memory, then compare it with
the template section.

# Revision Drill 15

### Recall

Without looking at the earlier sections, answer these mentally:

1.  What are the three pointers used in iterative reversal?
2.  What does `fast` do compared with `slow`?
3.  Why is `slow == fast` used for cycle detection?
4.  When is a dummy node useful?
5.  Why is `ArrayDeque` useful for stack and queue problems?
6.  What does LIFO mean?
7.  What does FIFO mean?
8.  What clues suggest a monotonic stack?
9.  Why is a queue natural for BFS?
10. What is the complexity of the standard O(n) linked-list templates?

**Coding prompt:** write one template from memory, then compare it with
the template section.

# Revision Drill 16

### Recall

Without looking at the earlier sections, answer these mentally:

1.  What are the three pointers used in iterative reversal?
2.  What does `fast` do compared with `slow`?
3.  Why is `slow == fast` used for cycle detection?
4.  When is a dummy node useful?
5.  Why is `ArrayDeque` useful for stack and queue problems?
6.  What does LIFO mean?
7.  What does FIFO mean?
8.  What clues suggest a monotonic stack?
9.  Why is a queue natural for BFS?
10. What is the complexity of the standard O(n) linked-list templates?

**Coding prompt:** write one template from memory, then compare it with
the template section.

# Revision Drill 17

### Recall

Without looking at the earlier sections, answer these mentally:

1.  What are the three pointers used in iterative reversal?
2.  What does `fast` do compared with `slow`?
3.  Why is `slow == fast` used for cycle detection?
4.  When is a dummy node useful?
5.  Why is `ArrayDeque` useful for stack and queue problems?
6.  What does LIFO mean?
7.  What does FIFO mean?
8.  What clues suggest a monotonic stack?
9.  Why is a queue natural for BFS?
10. What is the complexity of the standard O(n) linked-list templates?

**Coding prompt:** write one template from memory, then compare it with
the template section.

# Revision Drill 18

### Recall

Without looking at the earlier sections, answer these mentally:

1.  What are the three pointers used in iterative reversal?
2.  What does `fast` do compared with `slow`?
3.  Why is `slow == fast` used for cycle detection?
4.  When is a dummy node useful?
5.  Why is `ArrayDeque` useful for stack and queue problems?
6.  What does LIFO mean?
7.  What does FIFO mean?
8.  What clues suggest a monotonic stack?
9.  Why is a queue natural for BFS?
10. What is the complexity of the standard O(n) linked-list templates?

**Coding prompt:** write one template from memory, then compare it with
the template section.

# Revision Drill 19

### Recall

Without looking at the earlier sections, answer these mentally:

1.  What are the three pointers used in iterative reversal?
2.  What does `fast` do compared with `slow`?
3.  Why is `slow == fast` used for cycle detection?
4.  When is a dummy node useful?
5.  Why is `ArrayDeque` useful for stack and queue problems?
6.  What does LIFO mean?
7.  What does FIFO mean?
8.  What clues suggest a monotonic stack?
9.  Why is a queue natural for BFS?
10. What is the complexity of the standard O(n) linked-list templates?

**Coding prompt:** write one template from memory, then compare it with
the template section.

# Revision Drill 20

### Recall

Without looking at the earlier sections, answer these mentally:

1.  What are the three pointers used in iterative reversal?
2.  What does `fast` do compared with `slow`?
3.  Why is `slow == fast` used for cycle detection?
4.  When is a dummy node useful?
5.  Why is `ArrayDeque` useful for stack and queue problems?
6.  What does LIFO mean?
7.  What does FIFO mean?
8.  What clues suggest a monotonic stack?
9.  Why is a queue natural for BFS?
10. What is the complexity of the standard O(n) linked-list templates?

**Coding prompt:** write one template from memory, then compare it with
the template section.

# Revision Drill 21

### Recall

Without looking at the earlier sections, answer these mentally:

1.  What are the three pointers used in iterative reversal?
2.  What does `fast` do compared with `slow`?
3.  Why is `slow == fast` used for cycle detection?
4.  When is a dummy node useful?
5.  Why is `ArrayDeque` useful for stack and queue problems?
6.  What does LIFO mean?
7.  What does FIFO mean?
8.  What clues suggest a monotonic stack?
9.  Why is a queue natural for BFS?
10. What is the complexity of the standard O(n) linked-list templates?

**Coding prompt:** write one template from memory, then compare it with
the template section.

# Revision Drill 22

### Recall

Without looking at the earlier sections, answer these mentally:

1.  What are the three pointers used in iterative reversal?
2.  What does `fast` do compared with `slow`?
3.  Why is `slow == fast` used for cycle detection?
4.  When is a dummy node useful?
5.  Why is `ArrayDeque` useful for stack and queue problems?
6.  What does LIFO mean?
7.  What does FIFO mean?
8.  What clues suggest a monotonic stack?
9.  Why is a queue natural for BFS?
10. What is the complexity of the standard O(n) linked-list templates?

**Coding prompt:** write one template from memory, then compare it with
the template section.

# Revision Drill 23

### Recall

Without looking at the earlier sections, answer these mentally:

1.  What are the three pointers used in iterative reversal?
2.  What does `fast` do compared with `slow`?
3.  Why is `slow == fast` used for cycle detection?
4.  When is a dummy node useful?
5.  Why is `ArrayDeque` useful for stack and queue problems?
6.  What does LIFO mean?
7.  What does FIFO mean?
8.  What clues suggest a monotonic stack?
9.  Why is a queue natural for BFS?
10. What is the complexity of the standard O(n) linked-list templates?

**Coding prompt:** write one template from memory, then compare it with
the template section.

# Revision Drill 24

### Recall

Without looking at the earlier sections, answer these mentally:

1.  What are the three pointers used in iterative reversal?
2.  What does `fast` do compared with `slow`?
3.  Why is `slow == fast` used for cycle detection?
4.  When is a dummy node useful?
5.  Why is `ArrayDeque` useful for stack and queue problems?
6.  What does LIFO mean?
7.  What does FIFO mean?
8.  What clues suggest a monotonic stack?
9.  Why is a queue natural for BFS?
10. What is the complexity of the standard O(n) linked-list templates?

**Coding prompt:** write one template from memory, then compare it with
the template section.

# Revision Drill 25

### Recall

Without looking at the earlier sections, answer these mentally:

1.  What are the three pointers used in iterative reversal?
2.  What does `fast` do compared with `slow`?
3.  Why is `slow == fast` used for cycle detection?
4.  When is a dummy node useful?
5.  Why is `ArrayDeque` useful for stack and queue problems?
6.  What does LIFO mean?
7.  What does FIFO mean?
8.  What clues suggest a monotonic stack?
9.  Why is a queue natural for BFS?
10. What is the complexity of the standard O(n) linked-list templates?

**Coding prompt:** write one template from memory, then compare it with
the template section.

# Revision Drill 26

### Recall

Without looking at the earlier sections, answer these mentally:

1.  What are the three pointers used in iterative reversal?
2.  What does `fast` do compared with `slow`?
3.  Why is `slow == fast` used for cycle detection?
4.  When is a dummy node useful?
5.  Why is `ArrayDeque` useful for stack and queue problems?
6.  What does LIFO mean?
7.  What does FIFO mean?
8.  What clues suggest a monotonic stack?
9.  Why is a queue natural for BFS?
10. What is the complexity of the standard O(n) linked-list templates?

**Coding prompt:** write one template from memory, then compare it with
the template section.

# Revision Drill 27

### Recall

Without looking at the earlier sections, answer these mentally:

1.  What are the three pointers used in iterative reversal?
2.  What does `fast` do compared with `slow`?
3.  Why is `slow == fast` used for cycle detection?
4.  When is a dummy node useful?
5.  Why is `ArrayDeque` useful for stack and queue problems?
6.  What does LIFO mean?
7.  What does FIFO mean?
8.  What clues suggest a monotonic stack?
9.  Why is a queue natural for BFS?
10. What is the complexity of the standard O(n) linked-list templates?

**Coding prompt:** write one template from memory, then compare it with
the template section.

# Revision Drill 28

### Recall

Without looking at the earlier sections, answer these mentally:

1.  What are the three pointers used in iterative reversal?
2.  What does `fast` do compared with `slow`?
3.  Why is `slow == fast` used for cycle detection?
4.  When is a dummy node useful?
5.  Why is `ArrayDeque` useful for stack and queue problems?
6.  What does LIFO mean?
7.  What does FIFO mean?
8.  What clues suggest a monotonic stack?
9.  Why is a queue natural for BFS?
10. What is the complexity of the standard O(n) linked-list templates?

**Coding prompt:** write one template from memory, then compare it with
the template section.

# Revision Drill 29

### Recall

Without looking at the earlier sections, answer these mentally:

1.  What are the three pointers used in iterative reversal?
2.  What does `fast` do compared with `slow`?
3.  Why is `slow == fast` used for cycle detection?
4.  When is a dummy node useful?
5.  Why is `ArrayDeque` useful for stack and queue problems?
6.  What does LIFO mean?
7.  What does FIFO mean?
8.  What clues suggest a monotonic stack?
9.  Why is a queue natural for BFS?
10. What is the complexity of the standard O(n) linked-list templates?

**Coding prompt:** write one template from memory, then compare it with
the template section.

# Revision Drill 30

### Recall

Without looking at the earlier sections, answer these mentally:

1.  What are the three pointers used in iterative reversal?
2.  What does `fast` do compared with `slow`?
3.  Why is `slow == fast` used for cycle detection?
4.  When is a dummy node useful?
5.  Why is `ArrayDeque` useful for stack and queue problems?
6.  What does LIFO mean?
7.  What does FIFO mean?
8.  What clues suggest a monotonic stack?
9.  Why is a queue natural for BFS?
10. What is the complexity of the standard O(n) linked-list templates?

**Coding prompt:** write one template from memory, then compare it with
the template section.
