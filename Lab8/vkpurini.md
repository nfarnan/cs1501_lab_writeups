# Lab 8 Writeup

**Author:** Vivek Purini

---

## Valid Parentheses

**LeetCode Problem:** [20. Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)

## Solution

```python
class Solution:
    def isValid(self, s):
        stack = []
        matching = {')': '(', '}': '{', ']': '['}

        for char in s:
            if char in '({[':
                stack.append(char)
            else:
                if not stack or stack[-1] != matching[char]:
                    return False
                stack.pop()

        return len(stack) == 0
```

---

## What I Did

### Data Structures Used
- **Stack** (`list` in Python) — stores unmatched opening brackets as we scan left to right
- **Hash map** (`matching` dict) — maps each closing bracket to its expected opening counterpart

### Step-by-Step Logic

1. **Initialize** an empty stack and a dictionary mapping each closing bracket to its matching opener.
2. **Iterate** over every character in `s`:
   - If it is an **opening bracket** (`(`, `{`, `[`), push it onto the stack.
   - If it is a **closing bracket** (`)`, `}`, `]`):
     - Check if the stack is **empty** — if so, there is no matching opener, return `False`.
     - Check if the **top of the stack** matches the expected opener from the dictionary — if not, the brackets are mismatched or out of order, return `False`.
     - Otherwise, **pop** the top of the stack (the pair is matched).
3. After the loop, return `True` only if the stack is **empty** (no unmatched openers remain).


---

## Runtime Analysis

### Time Complexity — O(n)
- We iterate over the string exactly **once** — `n` characters total.
- Each character triggers at most one `push` or one `pop`, both O(1) for a Python list.
- Dictionary lookup (`matching[char]`) is O(1).
- **Total: O(n)**

### Space Complexity — O(n)
- In the worst case (e.g., `"(((((("`), every character is an opener and all get pushed onto the stack.
- The stack can grow to at most `n` elements.
- The `matching` dictionary is fixed size (3 entries) → O(1).
- **Total: O(n)**
