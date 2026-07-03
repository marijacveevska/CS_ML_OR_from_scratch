# Track 1: Python — Learning Schedule (Exact Daily Plan)

**Weekly slots:** Wed / Fri / Sat / Sun, 7–9am (8h/week). Sunday +2h when available = buffer/review, not new material.

Every session below tells you: the exact source + chapter/section, and the exact thing to practice. No research required when you sit down.

---

## PHASE 1 — Python fundamentals, OOP, patterns, data stack

### Week 1 — Collections: mutability, complexity, comprehensions

**Wed (2h) — Lists & tuples**
- Read: *Fluent Python* 2nd ed., **Ch. 2 "An Array of Sequences"** — sections "Overview of Built-In Sequences" through "Tuples Are Not Just Immutable Lists"
- Practice (write these yourself, no lookup needed):
  1. Write a function that takes a list and returns a new list with duplicates removed, preserving order (no `set()` allowed — do it manually first, then again with a comprehension).
  2. Show with `id()` that appending to a list doesn't change its identity, but `list = list + [x]` does.
  3. Write a tuple-unpacking example using `*` to grab first, last, and middle elements of a list of 6 items.

**Fri (2h) — Dicts & sets**
- Read: *Fluent Python* **Ch. 3 "Dictionaries and Sets"** — sections "Modern dict Syntax" through "Set Theory" (skip the hash table internals subsection for now, come back to it later if curious)
- Practice:
  1. Given a sentence (string), build `{word: length}` using a dict comprehension.
  2. Given two lists of equal length (`keys`, `values`), build a dict, then a **set** of only the values that appear more than once.
  3. Merge two dicts where the second should override the first on key conflicts, using `|` (Python 3.9+ syntax) — check it behaves as expected.

**Sat (2h) — Comprehensions deep dive**
- Read: *Fluent Python* **Ch. 2**, section "List Comprehensions and Generator Expressions" (re-read closely this time) + "Cartesian Products"
- Practice — do all 6, comprehension-only (no explicit for-loops):
  1. Flatten a list of lists (e.g. `[[1,2],[3,4]]` → `[1,2,3,4]`).
  2. Build a dict `{n: n**2}` for even numbers only, from `range(20)`.
  3. Transpose a matrix (list of lists) using a **nested** comprehension.
  4. Given a string, build `{char: count}` frequency dict.
  5. Cartesian product: given `colors = ['red','blue']` and `sizes = ['S','M']`, produce all `(color, size)` tuples.
  6. Given a list of dicts (e.g. `[{'name':'a','age':30}, ...]`), extract a list of just the names where age > 25.

**Sun (2h) — Complexity + consolidation**
- Read: [wiki.python.org/moin/TimeComplexity](https://wiki.python.org/moin/TimeComplexity) — the whole page, it's short. Focus especially on: list (index, append, insert, pop, contains), dict (get, set, delete), set operations.
- Practice: write out from memory (then check yourself against the page) the Big-O of: `list.append()`, `list.insert(0, x)`, `x in list`, `x in set`, `dict[key]` lookup, `dict[key] = val`. Write one sentence explaining *why* `x in list` is O(n) but `x in set` is O(1) — this should reference hashing.
- If +2h: redo Wednesday's exercise 1 (dedup) using `dict.fromkeys()` and compare readability/speed to your manual version.

---

### Week 2 — Functions, closures, decorators

**Wed (2h) — First-class functions & closures**
- Read: *Fluent Python* **Ch. 7 "Functions as First-Class Objects"** — sections "Treating a Function Like an Object" through "From Positional to Keyword-Only Parameters" (this covers `*args`/`**kwargs` directly)
- Practice:
  1. Write a function `apply_twice(f, x)` that applies `f` to `x` twice.
  2. Write a function `make_multiplier(n)` that returns a function multiplying its input by `n` (a closure) — verify with `make_multiplier(3)(10) == 30`.
  3. Write a function `summarize(*args, **kwargs)` that prints all positional args and all keyword args separately, then call it with a mix of both.

**Fri (2h) — Decorators**
- Read: *Fluent Python* **Ch. 9 "Decorators and Closures"** — sections "Decorators 101" through "Variable Scope Rules" and "Closures"
- Practice — write these 3 decorators from scratch (don't use `functools` yet):
  1. `@timer` — prints how long the wrapped function took to run.
  2. `@log_calls` — prints the function name and arguments every time it's called.
  3. `@memoize` — caches results by argument, so a slow recursive function (test with a naive `fibonacci(n)`) speeds up dramatically on repeat calls.

**Sat (2h) — Decorators continued: parametrized + functools**
- Read: *Fluent Python* **Ch. 9**, remaining sections: "Implementing a Simple Decorator" through "functools.wraps"
- Practice:
  1. Rewrite your `@log_calls` decorator using `functools.wraps` and confirm `__name__`/`__doc__` are preserved on the wrapped function (test by printing `wrapped_func.__name__` before/after the fix).
  2. Write a **parametrized** decorator `@repeat(n)` that calls the wrapped function `n` times.
  3. Replace your hand-written `@memoize` from Friday with `functools.lru_cache` and confirm identical behavior.

**Sun (2h) — Consolidation**
- No new reading.
- Practice: pick any small script you've written before (or write a 10–15 line one now, e.g. a function that processes a list of numbers) and apply at least 2 of this week's decorators to it. Goal: it should feel natural, not like assembling unfamiliar syntax.
- If +2h: start Monday's reading early (Ch. 6 "Object References, Mutability, and Recycling" — this bridges into next week nicely, sections "Variables Are Not Boxes" through "Copies Are Shallow by Default").

---

### Week 3 — Classes, dunder methods, class design for pipelines

**Wed (2h) — The Python Data Model**
- Read: *Fluent Python* **Ch. 1 "The Python Data Model"** — the full chapter (it's short, ~15 pages), especially "A Pythonic Card Deck" and "Overview of Special Methods"
- Practice:
  1. Build the `FrenchDeck` class from the chapter yourself (don't copy-paste — type it from the concept) with `__len__` and `__getitem__`.
  2. Confirm it supports `len(deck)`, indexing `deck[0]`, slicing `deck[:3]`, and iteration (`for card in deck`) — note that you get iteration and slicing *for free* from just implementing `__getitem__`. Write a comment explaining why.

**Fri (2h) — A Pythonic Object: more dunder methods**
- Read: *Fluent Python* **Ch. 11 "A Pythonic Object"** — sections on `__repr__`, `__eq__`, `__hash__`, and object representation (skim the format-spec-mini-language parts, not essential right now)
- Practice: build a `Vector2D` class with:
  1. `__init__(self, x, y)`
  2. `__repr__` (should return something like `Vector2D(3, 4)`)
  3. `__eq__` (two vectors equal if x and y match)
  4. `__add__` (vector addition returns a new `Vector2D`)
  5. Test: create two vectors, add them, print the result, and confirm equality comparison works.

**Sat (2h) — Class design: composition vs inheritance**
- Read: *Fluent Python* **Ch. 14 "Inheritance: For Better or Worse"** — sections "The super() Function" and "Multiple Inheritance and Method Resolution Order" (just enough to understand the tradeoffs — this chapter argues for composition over inheritance in most cases, which is directly relevant to pipeline design)
- Practice:
  1. Design a base class `Transform` with a method `apply(self, data)` that raises `NotImplementedError`.
  2. Write 2 subclasses: `Normalize` and `ClipOutliers`, each implementing `apply()` differently (can work on a plain Python list of numbers, no need for numpy yet).
  3. Write a `Pipeline` class that holds a list of `Transform` objects and applies them in sequence via composition (the `Pipeline` *has* transforms, rather than inheriting from them).

**Sun (2h) — Build a mini pipeline end-to-end**
- No new reading.
- Practice: extend Saturday's `Pipeline` class — add a `__repr__` so printing a pipeline shows the steps in order, and add `__len__` returning the number of steps. Run a toy list of numbers through a 3-step pipeline and print the result at each stage.
- If +2h: read *Fluent Python* **Ch. 17**, section "Why Sequences Are Iterable: The `iter` Function" through "Iterables Versus Iterators" — this sets up Week 4 Wednesday.

---

### Week 4 — Pythonic design patterns

**Wed (2h) — Iterators & Generators**
- Read: *Fluent Python* **Ch. 17 "Iterators, Generators, and Classic Coroutines"** — sections "Sentence Classes with `__iter__`" through "Sentence Take #3: A Generator Function" (this shows the *same* problem solved as a classic iterator class, then as a generator — very useful side-by-side)
- Practice:
  1. Write a custom iterator **class** for Fibonacci numbers (with `__iter__` and `__next__`) that yields the first N values.
  2. Write the **same thing** as a generator function using `yield` — compare the amount of code.
  3. Write a generator function `batch(iterable, size)` that yields chunks of a given size from any iterable (useful pattern for ML data loading).

**Fri (2h) — Decorator pattern & Observer**
- Read: [refactoring.guru/design-patterns/decorator/python/example](https://refactoring.guru/design-patterns/decorator/python/example) and [refactoring.guru/design-patterns/observer/python/example](https://refactoring.guru/design-patterns/observer/python/example)
- Practice:
  1. Decorator pattern (structural, not the `@` syntax): build a `DataSource` class with a `read()` method, then wrap it with a `CompressionDecorator` and `EncryptionDecorator` that each add behavior around `read()` without modifying `DataSource` itself.
  2. Observer pattern: build a `Subject` class (e.g. `TrainingRun`) that notifies a list of `Observer` objects (e.g. `ConsoleLogger`, `MetricsTracker`) whenever `notify(epoch, loss)` is called.

**Sat (2h) — Builder pattern**
- Read: [refactoring.guru/design-patterns/builder/python/example](https://refactoring.guru/design-patterns/builder/python/example)
- Practice: build a `ModelConfigBuilder` that lets you chain calls like `.set_learning_rate(0.01).set_layers(3).set_optimizer("adam").build()`, returning a finished config object at the end. Confirm method chaining works (each setter returns `self`).

**Sun (2h) — Fluent Python's take on patterns**
- Read: *Fluent Python* **Ch. 10 "Design Patterns with First-Class Functions"** — sections "Case Study: Refactoring Strategy" through "Decorator-Enhanced Strategy Pattern" (this shows how Python's first-class functions make some classic OOP patterns, like Strategy, unnecessary as full classes — important so you don't over-engineer later)
- Practice: take your `Transform`/`Pipeline` classes from Week 3 and refactor `Transform` from a class hierarchy into plain functions + a `Pipeline` that just holds a list of callables. Compare which version you find more readable.
- If +2h: buffer — revisit whichever of this week's 4 patterns felt least solid.

---

### Week 5 — Data stack refresher (NumPy, Pandas, Matplotlib)

**Wed (2h) — NumPy**
- Read: *Python Data Science Handbook* — **"Introduction to NumPy"** chapter, sections on array creation, indexing/slicing, and **broadcasting** specifically (this is the part most people are rusty on)
- Practice: given a 2D numpy array (make one up, e.g. `np.random.rand(5,5)`), practice: boolean masking (select all values > 0.5), broadcasting a 1D array against it, and vectorizing a function that would otherwise need a Python loop.

**Fri (2h) — Pandas**
- Read: *Python Data Science Handbook* — **"Data Manipulation with Pandas"** chapter, sections on indexing/selection, **groupby**, and **merge/join**
- Practice: take any small tabular dataset (make one up as a dict of lists, e.g. sales by region/month), load into a DataFrame, and practice: groupby + aggregate, a merge with another small DataFrame, and a pivot table.

**Sat (2h) — Matplotlib**
- Read: *Python Data Science Handbook* — **"Visualization with Matplotlib"** chapter, sections on basic line/scatter plots and subplots
- Practice: plot a simple time series (fake data), then a 2x2 grid of subplots showing different views of the same fake dataset.

**Sun (2h) — Buffer / consolidation**
- This week should run fast given your background — use spare time to go back over any Phase 1 exercise that felt shaky rather than rushing into Phase 2. If everything felt solid, do a self-check: without opening the book, write a decorator, a generator function, and a class with 2 dunder methods from memory.

---

## PHASE 2 — Data Structures (Weeks 6–8)

Primary sources per session: *A Common-Sense Guide to Data Structures and Algorithms*, 2nd ed. (Wengrow) for concept, [neetcode.io/roadmap](https://neetcode.io/roadmap) for structure, and named LeetCode problems for practice (search the exact title on leetcode.com — they're unambiguous by name).

### Week 6 — Arrays, hash maps, stacks, queues

**Wed** — Read Wengrow **Ch. 3 "Big O Notation"** + **Ch. 7 "Blazing Fast Lookup with Hash Tables"**. Practice: LeetCode *Two Sum*, *Contains Duplicate*, *Valid Anagram*.

**Fri** — Read Wengrow's chapter on stacks **Ch. 9(Crafting elegant code with "Stacks and Queues")**. Practice: *Valid Parentheses*, *Min Stack*.

**Sat** — Same chapter, queues/deques half. Practice: *Evaluate Reverse Polish Notation*, *Generate Parentheses*.

**Sun** — Practice mix: *Group Anagrams*, *Top K Frequent Elements*, *Product of Array Except Self*.

### Week 7 — Trees & recursion

**Wed** — Read Wengrow's recursion chapter **Ch. 10** in full. Practice: write `factorial(n)` and `fibonacci(n)` recursively, then trace the call stack on paper for `fibonacci(5)`.

**Fri** — Read Wengrow **Ch. 14 "Node-Based Data Structures"** (binary trees). Practice: *Invert Binary Tree*, *Maximum Depth of Binary Tree*.

**Sat** — Same chapter continued (BSTs) + Wengrow **Ch. 15** (BST operations). Practice: *Same Tree*, *Subtree of Another Tree*, *Validate Binary Search Tree*.

**Sun** — Practice: *Binary Tree Level Order Traversal*, *Lowest Common Ancestor of a BST*, *Kth Smallest Element in a BST*.

### Week 8 — Graphs

**Wed** — Read Wengrow's graphs chapter **Ch. 18** (near the end of the book) + [NeetCode roadmap: Graphs section](https://neetcode.io/roadmap). Practice: *Number of Islands*.

**Fri** — Practice BFS specifically: *Clone Graph*, *Max Area of Island*.

**Sat** — Practice DFS specifically: *Pacific Atlantic Water Flow*, *Course Schedule*.

**Sun** — Practice mix: *Number of Connected Components*, *Graph Valid Tree*.

---

## PHASE 3 — Algorithm Patterns (Weeks 9–12)

Source for all sessions: [neetcode.io/roadmap](https://neetcode.io/roadmap) (watch the pattern-intro video for each), practice via named LeetCode problems.

### Week 9
- **Wed — Two pointers:** *Valid Palindrome*, *Two Sum II*, *3Sum*
- **Fri — Sliding window:** *Best Time to Buy and Sell Stock*, *Longest Substring Without Repeating Characters*
- **Sat — Binary search:** *Binary Search*, *Search in Rotated Sorted Array*, *Find Minimum in Rotated Sorted Array*
- **Sun — Mixed practice:** *Container With Most Water*, *Longest Repeating Character Replacement*, *Koko Eating Bananas*

### Week 10
- **Wed — Backtracking pt 1:** *Subsets*, *Combination Sum*
- **Fri — Backtracking pt 2:** *Permutations*, *Word Search*
- **Sat — DFS as a pattern (trees/graphs recap through this lens):** *Palindrome Partitioning*, *Letter Combinations of a Phone Number*
- **Sun — Mixed practice:** *N-Queens*, *Subsets II*

### Week 11
- **Wed — Hash map tricks:** *Longest Consecutive Sequence*, *Encode and Decode Strings*
- **Fri — BFS as a pattern:** *Binary Tree Right Side View* (revisit), *Rotting Oranges*
- **Sat — DP 1D pt 1:** *Climbing Stairs*, *House Robber*, *House Robber II*
- **Sun — DP 1D pt 2:** *Coin Change*, *Longest Increasing Subsequence*, *Word Break*

### Week 12
- **Wed — DP 2D pt 1:** *Unique Paths*, *Longest Common Subsequence*
- **Fri — DP 2D pt 2:** *Best Time to Buy/Sell Stock with Cooldown*, *Coin Change II*
- **Sat — Mixed review:** re-solve your 3 weakest problems from Weeks 9–11 (check your notes/memory for which ones took longest or needed the video)
- **Sun — Full mixed practice set + transition prep:** set up the tracking spreadsheet described below, ready for Phase 4

---

## PHASE 4 — NeetCode 150 (Week 13 onward)

- Go to [neetcode.io/practice](https://neetcode.io/practice), filter to the **NeetCode 150** list.
- **Tracking spreadsheet columns:** Problem name | Pattern tag | Date | Time taken | Solved unaided (Y/N) | Needs review (Y/N)
- **Easy problems:** no time pressure, ~3–4 per 2h session, goal is correctness + recognizing the pattern.
- **Medium problems:** 20-minute cap per attempt. If stuck at 20 min, watch the NeetCode video for that exact problem, understand it fully, then re-attempt unaided a few days later.
- **Every Sunday:** review the spreadsheet, re-attempt anything marked "needs review."
- Budget 8–10 weeks at your current pace — don't compress this; repetition on weak spots matters more than raw coverage.

---

## Notes
- Chapter numbers for *Fluent Python* are verified against the official 2nd edition table of contents. Wengrow chapter numbers are given where confirmed (3, 7, 14, 15); others are described by topic since exact numbering wasn't independently verified — the book's own TOC will get you there in seconds.
- If a session's reading runs long, cut it short and move to practice — the practice problems are the priority, the reading is scaffolding for them.
