# Lab 9: Min Cost to Climb Stairs
## Code
```java
class Solution {
    public int minCostClimbingStairs(int[] cost) {
        int n = cost.length;
        int[] currentPrice = new int[n+1]; // min cost to get to index cost.length, so need length cost.length+1
        for (int i = 2; i <= n; i++){
            int potentialStep1 = currentPrice[i-1]+cost[i-1];
            int potentialStep2 = currentPrice[i-2]+cost[i-2];
            currentPrice[i] = Math.min(potentialStep1, potentialStep2);
        }
        return currentPrice[n];
    }
}

// every time we want to step we should look at the 2 possibilities
// we can either go from 0 or 1 -> this is weird so we should do it from the middle
// so well grab whichever step length will be the smallest and have that be the current price to get to step i
// well keep grabbing whichever way that gets us to the top in the smallest amount of time
// do this until aura monster finishes climbing stairs and return currentPrice[n]
```
## Code Explanation
My code first creates an array to keep track of the current lowest price to get to step i. Then, I
iterate through the staircase array, looking at the previous possible steps (climbing 1 or 2 stairs)
and takes the lowest of them, saving the lowest price to get to i in currentPrice. Once the loop has
gone once or twice, it also compares the price to get to some step of the staircase + the cost to 
climb it (still saving result in currentPrice[i]). Once we get to i = n, we save the price to get 
past the staircase (index cost.length) which is what the problem wants. We then return this as
the min price to climb stairs.
## Time and Space Complexity
The time complexity is O(n) where n is the length of cost, as my program does only O(1) calls inside 
the loop, but my program does iterate through a loop of n length. The space complexity is O(n), as I
create a new array of length n to save the current price to get to a certain step of the staircase.
