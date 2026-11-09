## Lab 8: Valid Parenthesis
### Code
```java
 class Solution {
    public boolean isValid(String s) {
        LinkedList<Character> parenthesis = new LinkedList<Character>();
        for(char a : s.toCharArray()){
            if(a == '(' || a == '{' || a == '['){
                parenthesis.addFirst((Character)a); // add to top -> using as Stack
            } else if (!parenthesis.isEmpty()){
                Character currentHead = parenthesis.peek(); // look at top
                if(currentHead == '(' && a == ')'){
                    parenthesis.pop(); //-> remove top
                } else if (currentHead == '{' && a == '}'){
                    parenthesis.pop();
                } else if (currentHead == '[' && a == ']') {
                    parenthesis.pop();
                } else {
                    return false;
                }
            } else {
                return false;
            }
        }
        return parenthesis.isEmpty();
    }
}
```

### Code Explanation
I had remembered discussing this problem (or one similar to it) in 445 so I decided to use a similar approach. 
My goal was to use a stack to keep track of the previous parenthesis and compare it to the next one. If
the parenthesis is open, then we just add it. If it is closed, it has to match the most recently added open
parenthesis. If it does, we pop the open parenthesis stack and continue. If it does not, we know that it is not
valid and we end program and return false. After we have gone through the whole string, the string is valid if our stack 
is empty, and invalid if it is not.
### Time and Space Complexity
My program iterates through a string of length n, and performs only O(1) operations to each character.
Therefore, my time complexity is O(n). I initialize a linked list to store all of the open parenthesis,
which could be a maximum of O(n) space. While I could pre-emptively end the program if the linked list
grows past n/2, it would not affect the time complexity which would stay O(n).
