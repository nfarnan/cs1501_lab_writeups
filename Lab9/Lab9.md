# Lab 9 - Garfield Zhang

## Solution
```
class Solution {
    public int minCostClimbingStairs(int[] cost) {
        return Math.min(step(cost, 0), step(cost, 1));
    }

    private int step(int[] cost, int i) {
        if (i >= cost.length) {
            return 0;
        }

        int oneStep = step(cost, i + 1);
        int twoSteps = step(cost, i + 2);

        return cost[i] + Math.min(oneStep, twoSteps);
    }
}

```


### Explain
    Used recursion keep checking after we paid is it better to take 1 steps or 2 steps which will cost less.
    we kept calling after we paid taking 1 or 2 step then get the cost from the array cost[] after we take the step and compare the stair we land at after 1 step  2 step which cost less

## Time and Space Complexity
### time: 
O (2^n) recursion call kept checking we should taking 1 or two steps 
   

### Space
O(n) maximum recursive call    