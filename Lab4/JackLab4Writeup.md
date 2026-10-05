## Lab 4: Maximum Produce of Two Elements in Array
### Code
```
class Solution {
    public int maxProduct(int[] nums) {

        int greater = 0;
        int greatest = 1;
        for (int i = 0; i < nums.length; i++){
            if (nums[i] > greater){
                if (nums[i] > greatest) {
                    greater = greatest;
                    greatest = nums[i];
                } else {
                    greater = nums[i];
                }
            }
        }

        return (greatest-1) * (greater-1);
    }
}
```

### Code Explanation
This solution is pretty simple. First, I initialize 2 ints, greater and greatest, which will store the values of the 2nd and
1st largest values, respectively. They are initialized to 0 and 1 to fit the logic of the for loop; since we are guarunteed an
input array of at least 2 elements, it won't ever mistakenly return these. Then, the program iterates through nums and if it finds
a nums[i] that is greater than 'greater', if nums[i] is also greater than 'greatest' it will set 'greater' to 'greatest' and set greatest
to the new index. Otherwise, if it's greater than 'greater' but not 'greatest', nums[i] replaces greater instead. Then, it just
returns greatest-1 * greater-1, which is what we need for the solution.

### Time and Space Complexity
The time complexity is O(n), since the program iterates through nums 1 time. The only operations within the loop are O(1), 
and there are only O(1) operations outside the loop as well. The space complexity is also O(1), since we are just storing 2 values.
