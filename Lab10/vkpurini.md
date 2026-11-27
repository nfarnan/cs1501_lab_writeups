# Lab 10 Writeup

**Author:** Vivek Purini

---

## Print FooBar Alternately

**LeetCode Problem:** [1115. Print FooBar Alternately](https://leetcode.com/problems/print-foobar-alternately/)

## Solution

```python
import threading

class FooBar(object):
    def __init__(self, n):
        self.n = n
        self.foo_sem = threading.Semaphore(1)  # foo goes first
        self.bar_sem = threading.Semaphore(0)  # bar must wait

    def foo(self, printFoo):
        for i in range(self.n):
            self.foo_sem.acquire()
            printFoo()
            self.bar_sem.release()

    def bar(self, printBar):
        for i in range(self.n):
            self.bar_sem.acquire()
            printBar()
            self.foo_sem.release()
```

## Description

Two semaphores enforce alternating order. `foo_sem` starts at 1 so `foo` runs first; `bar_sem` starts at 0 so `bar` blocks. After each print, the thread releases the other's semaphore — creating a strict ping-pong between threads.

## Runtime and Memory Analysis

**Time complexity: O(n)** — each thread loops n times, O(1) work per iteration.

**Space complexity: O(1)** — two semaphores regardless of n.
