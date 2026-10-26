## Lab 6: Find the Town Judge
### Code

```java
// we could just make like 2 arrays and call it a day
// just save who is trusted and who is truster
// then do stuff based off of that

class Solution {
    public int findJudge(int n, int[][] trust) {

        if(n == 1){
            return 1;
        }

        int[] trusted = new int[n+1];
        boolean[] truster = new boolean[n+1];


        for (int i = 0; i < trust.length;i++){
            trusted[trust[i][1]] += 1;
            truster[trust[i][0]] = true;
        }

        for (int j = 1; j <= n; j++){
            if(trusted[j] == n-1 && truster[j] == false){
                return j;
            }
        }
        return -1;
    }
}
```

### Code Explanation
My code is fairly simple. If there is just 1 person in the town then that is the judge. Otherwise,
I make 2 arrays, truster and trusted, to keep track of both who cannot be a judge because they trust
someone else and who can be the judge because everyone else trusts them. I then iterate through
trust and update how many people trust the person at trust[i][1] and signify the person who
trusts them as a truster. After I am done iterating through this, I then go through every member
of the town and check if the rest of the town trusts them and if they are not a truster themselves.
If both of these conditions are met, we have found our judge. Otherwise, we have to keep searching.
If the program finds no one, then the loop ends and returns -1.
### Time and Space Complexity
Since my most time expensive operation is iterating through one dimension of trust[][] and also
iterating through my created trusted and truster arrays, my program is O(n+m) where m is the number 
of entries in trust[][] (the other dimension is constant) and n is the number of people in the town.
Since I create 2 arrays of length n to store both the trusters and the trusteds, my space complexity
is O(n) with the same n as above.

