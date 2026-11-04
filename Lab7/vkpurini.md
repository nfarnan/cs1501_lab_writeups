# Lab 7 Writeup

**Author:** Vivek Purini

---

## Flood Fill

**LeetCode Problem:** [733. Flood Fill](https://leetcode.com/problems/flood-fill/)

## Solution

```python
class Solution(object):
    def floodFill(self, image, sr, sc, color):
        original = image[sr][sc]  # save the color we're replacing
        if original == color:     # already the target color — nothing to do
            return image

        rows, cols = len(image), len(image[0])
        stack = [(sr, sc)]  # iterative DFS starting from the given pixel

        while stack:
            r, c = stack.pop()
            if r < 0 or r >= rows or c < 0 or c >= cols or image[r][c] != original:
                continue  # out of bounds or wrong color — skip
            image[r][c] = color  # recolor this pixel
            stack.append((r + 1, c))  # push all 4 neighbors
            stack.append((r - 1, c))
            stack.append((r, c + 1))
            stack.append((r, c - 1))

        return image
```

## Description

The problem is a flood fill — starting from a pixel, recolor it and all connected pixels of the same color to a new color. Connected means horizontally or vertically adjacent, not diagonal.

The edge case is when the starting pixel is already the target color. Without this check the algorithm would loop forever, recoloring pixels that are already `color` and pushing their neighbors endlessly.

The solution uses iterative DFS with a stack. Each pixel gets popped, checked (bounds + correct original color), recolored, and its 4 neighbors pushed onto the stack. Recoloring the pixel before pushing neighbors acts as the visited marker — once a pixel is set to `color` it no longer matches `original`, so it won't be processed again if it gets pushed twice.

## Runtime and Memory Analysis

**Time complexity: O(m × n)**

In the worst case every pixel in the grid gets visited once, so the loop runs at most m × n times.

**Space complexity: O(m × n)**

The stack can hold at most m × n entries in the worst case — if the entire grid is the same color and needs to be filled.
