# Lab 9 Writeup

**Author:** Vivek Purini

---

## Min Cost Climbing Stairs

**LeetCode Problem:** [746. Min Cost Climbing Stairs](https://leetcode.com/problems/min-cost-climbing-stairs/)

## Solution

```python
class Solution(object):
    def minCostClimbingStairs(self, cost):
        n = len(cost)
        dp = [0] * (n + 1)
        for i in range(2, n + 1):
            dp[i] = min(dp[i-1] + cost[i-1], dp[i-2] + cost[i-2])
        return dp[n]
```

## Description

The problem asks for the minimum cost to reach the top of a staircase, where you can start at step 0 or step 1 and climb one or two steps at a time. The top is the position just past the last step.

The key insight is that the minimum cost to reach any step `i` can only come from two places — the step directly below (`i-1`) or two steps below (`i-2`). That gives a simple recurrence: the cost to reach step `i` is the minimum of arriving from `i-1` (paying `cost[i-1]`) or arriving from `i-2` (paying `cost[i-2]`).

A `dp` array of size `n+1` stores the minimum cost to reach each position. The first two entries are 0 because you can start at either step 0 or step 1 for free. The loop fills in the rest and the answer is `dp[n]` — the cost to reach the top, which has no cost of its own.

## Runtime and Memory Analysis

**Time complexity: O(n)**

The loop runs from index 2 to n, visiting each step exactly once.

**Space complexity: O(n)**

The `dp` array holds n+1 values. This can be reduced to O(1) by keeping just the last two values instead of the full array, but the array version is clearer.
