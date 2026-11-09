# Lab 8: Valid Parentheses (LC #20)
Luke Douglas
## Code Solution
```java
class Solution {
    private static char matchingOpener(char c) {
        if (c == ')') return '(';
        if (c == '}') return '{';
        return '[';
    }

    private static boolean isEnder(char c) {
        return c == ')' || c == ']' || c == '}';
    }

    public boolean isValid(String s) {
        Deque<Character> stack = new ArrayDeque<>();
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if (isEnder(c)) {
                try {
                    char stackChar = stack.pop();
                    if (stackChar != matchingOpener(c)) {
                        return false;
                    }
                } catch (Exception e) {
                    return false;
                }
            } else {
                stack.push(c);
            }
        }
        return stack.isEmpty();
    }
}
```
## Code Explanation
First, I have some helper functions to handle matching brackets to each other. The `matchingOpener` function takes in a closing bracket (`')'`, `']'`, or `'}'`) and returns the corresponding opening bracket. The `isEnder` function takes in a character and returns `true` if it is a closing bracket.
On to the main function. First, I initialize a stack to handle our validation. Then, I iterate over the string. For each character `c` in `s`, if `c` is an closing bracket, then I pop the most recently added unclosed opening character off the stack. If it's the correct one, we continue on; that bracket pair has been handled. If it's the incorrect opening bracket, we return false. If the stack is empty, we catch the exception and return false (there's a closing bracket with no opening bracket). If `c` is an opening bracket, we simply push it onto the stack. Then, after going over all characters, if the stack is not empty, that means there is an opening bracket that hasn't been closed, so we return false. Otherwise, we return true, because our string is valid.
## Complexity Analysis
My function has a time complexity of $O(n)$, where $n$ is the number of characters in `s`. In the worst case, all the characters in the string are opening brackets, so we have to iterate over the whole string doing $n$ consecutive pushes. My `ArrayDeque` will have to resize during some of these pushes, but asymptotically, this is $O(1)$, so it's okay.
My function has a space complexity of $O(n)$. The worst case is the same: all opening brackets. Our `ArrayDeque` will have to store all $n$ characters at once and will take up space bounded above by $2n$, because that's how it does resizing. Everything takes up a constant amount of space no matter what the input is.