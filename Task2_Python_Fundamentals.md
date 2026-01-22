# Task 2 – Python, Data Structures, Algorithms & System Design

This document contains answers to Task 2, covering Python internals, data structures,
algorithms, concurrency, and system design concepts. The focus is on clarity,
correctness, and practical understanding.

---

## Section A: Advanced Python Internals

### Q1. Explain Python memory management, reference counting, and circular references

Python manages memory using a private heap. Every object maintains a reference count,
which tracks how many variables point to it. When the reference count reaches zero,
the memory is freed.

Circular references occur when two or more objects reference each other, preventing
their reference counts from reaching zero. Python handles this using a garbage
collector that detects and cleans up such cycles.

---

### Q2. Explain the Global Interpreter Lock (GIL) and how to mitigate its impact

The GIL ensures that only one thread executes Python bytecode at a time. This simplifies
memory management and avoids race conditions but limits CPU-bound multi-threading.

Mitigations:
- Use multiprocessing for CPU-bound tasks
- Use asyncio for I/O-bound tasks
- Use C extensions (e.g., NumPy) that release the GIL

---

### Q3. Difference between __new__ vs __init__ and staticmethod vs classmethod

`__new__` creates the object, while `__init__` initializes it.

```python
class Example:
    def __new__(cls):
        return super().__new__(cls)

    def __init__(self):
        self.value = 10
staticmethod does not access class or instance, while classmethod receives the class.

class Demo:
    @staticmethod
    def add(a, b):
        return a + b

    @classmethod
    def name(cls):
        return cls.__name__

Q4. Implement a custom context manager
class FileManager:
    def __enter__(self):
        self.file = open("data.txt")
        return self.file

    def __exit__(self, exc_type, exc, traceback):
        self.file.close()


Context managers ensure proper resource cleanup.

Q5. Explain descriptors and implement one for validating positive integers

Descriptors control attribute access.

class Positive:
    def __set__(self, obj, value):
        if value <= 0:
            raise ValueError("Value must be positive")
        obj.__dict__["value"] = value


Used in frameworks like Django for validation.

Q6. Explain decorators with arguments and write a retry decorator

Decorators wrap functions to add behavior.

def retry(times):
    def decorator(func):
        def wrapper(*args, **kwargs):
            for _ in range(times):
                try:
                    return func(*args, **kwargs)
                except Exception:
                    pass
        return wrapper
    return decorator


Useful for retrying network or database calls.

Q7. Explain generators vs iterators and memory implications

Generators produce values lazily using yield, making them memory-efficient compared
to iterators that store all values in memory.

Section B: Data Structures & Design
Q8. Design an LRU Cache with O(1) operations

An LRU cache uses:

HashMap for fast access

Doubly Linked List to track usage order

Both get and put operations run in O(1) time.

Q9. Implement a Trie (Prefix Tree)
class Trie:
    def __init__(self):
        self.children = {}
        self.end = False


Tries are used for autocomplete and prefix searches.

Q10. Explain heap data structure and implement a min-heap

A heap is a complete binary tree.

import heapq
heap = []
heapq.heappush(heap, 5)
heapq.heappop(heap)


Insertion and deletion take O(log n).

Q11. Design a data structure with insert, delete, and getRandom in O(1)

Use:

List for random access

Dictionary for index tracking

Q12. Explain immutability and its role in concurrency

Immutable objects cannot change after creation, making them thread-safe by default.
They help prevent race conditions in concurrent systems.

Q13. Explain consistent hashing and real-world use cases

Consistent hashing minimizes re-mapping when nodes are added or removed. It is widely
used in distributed caching and load balancing systems.

Section C: Algorithms
Q14. Find the Kth largest element efficiently

Use a min-heap of size K or Quickselect.

Average Time: O(n)

Q15. Implement Quick Sort and discuss complexity

Quick Sort uses divide-and-conquer.

Average: O(n log n)

Worst: O(n²)

Q16. Longest substring without repeating characters

Solved using sliding window.

Time: O(n)
Space: O(n)

Q17. Detect cycles in directed and undirected graphs

Directed: DFS with recursion stack

Undirected: Union-Find

Q18. Implement topological sorting and explain use cases

Topological sorting orders nodes in a DAG. Used in task scheduling and dependency
resolution.

Q19. Solve number of islands problem

Traverse the grid using DFS/BFS and count connected components.

Time: O(m × n)

Q20. Explain dynamic programming and solve coin change

Dynamic programming breaks problems into subproblems.

dp[i] = min(dp[i], dp[i - coin] + 1)

Section D: Performance & Concurrency
Q21. Explain threading vs multiprocessing vs asyncio

Threading: I/O-bound tasks

Multiprocessing: CPU-bound tasks

Asyncio: High-concurrency I/O

Q22. Write an example where asyncio outperforms threading

Asyncio handles thousands of I/O requests using a single thread, while threading
creates overhead with multiple threads.

Q23. Explain profiling and optimizing Python applications

Tools:

cProfile

line_profiler

memory_profiler

Used to identify performance bottlenecks.

Section E: System Design
Q24. Design a URL shortener system

Components:

API service

Base62 encoding

Database

Cache (Redis)

Challenges include collisions and scalability.

Q25. Design a high-throughput log analytics system

Architecture:
Producers → Kafka → Stream Processing → Storage

Used for monitoring, analytics, and alerting.