# Nat205 Implementation

```
class Solution:
    def minCostClimbingStairs(self, cost: list[int]) -> int:
        n = len(cost)+1
        dp = [0] * n
        for i in range(2, n):
            dp[i] = min(dp[i-1] + cost[i-1], dp[i-2] + cost[i-2])
        
        return dp[-1]
```

# How my implementation works

The problem gives us an array where cost[i] is the cost of stepping on step i, and once we pay we can climb either 1 or 2 steps. We can start at step 0 or step 1, and we need to return the minimum cost to reach the top, which is one step past the last index. Since the cheapest way to reach a step depends on the cheapest way to reach the two steps before it, we are solving the same smaller problems over and over again, so I used dynamic programming. I made a dp array of size len(cost) + 1, where dp[i] is the minimum cost to reach step i, and the last spot is the top. dp[0] and dp[1] stay 0 because we can start on either of them for free. Then for every step from 2 to the top, I take the cheaper option between coming from one step below (dp[i-1] + cost[i-1]) or from two steps below (dp[i-2] + cost[i-2]). Finally, I return dp[-1], which is the minimum cost to reach the top.


# Runtime and Memory Analysis

## Runtime
I loop through the steps once and each step does a constant amount of work, so the final runtime is O(N) w/r N is the length of cost.


## Space
The dp array has N + 1 spots, so the space is O(N). This could be O(1) if I only kept the last two values in two variables instead of the whole array, since each step only looks back two steps.
