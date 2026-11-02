## Lab 7: Flood Fill
### Code
```java
class Solution {
    public int[][] floodFill(int[][] image, int sr, int sc, int color) {
        int startingColor = image[sr][sc];
        recurFlood(image, sr, sc, startingColor, color);
        return image;
        // check top
        // check right
        // check bottom
        // check left
        // if they are successful, jump there and recur
    }
    private void recurFlood(int[][] image, int sr, int sc, int startingColor, int floodColor){
        if (image[sr][sc] == floodColor){
            return;
        }
        if (image[sr][sc] == startingColor){
            image[sr][sc] = floodColor;

            if (image.length > sr+1){
                recurFlood(image, sr+1, sc, startingColor, floodColor);
            }
            if (image[0].length > sc+1){
                recurFlood(image, sr, sc+1, startingColor, floodColor);
            }
            if (sr > 0){
                recurFlood(image, sr-1, sc, startingColor, floodColor);
            }
            if (sc > 0){
                recurFlood(image, sr, sc-1, startingColor, floodColor);
            }
        }
    } 
}
```
### Code Explanation
To solve this problem, I created a function recurFlood, which has the same parameters as the original
function but differentiates the starting color and the flood color. My program uses this new function
to do nearly all of the logic. How it works is basically, if image[sr][sc] is currently on the starting 
color, my function will color in the square with the flood color. Then, if the square was colored in,
my function will attempt to recur to every adjacent square if the square is within the bounds of the 
array image[][].

### Time and Space Complexity
My program has a time complexity of O(n * m), where n is the number of rows and m is the number of 
columns. My program has a space complexity of O(n * m) with the same n and m as above, since recursion
contributes towards space complexity and my program could recur through the entire 2d array.
