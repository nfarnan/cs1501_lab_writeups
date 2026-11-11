# My Implementation 
```class Solution:
    def isValid(self, s: str) -> bool:
        parens = {'(':')', '[':']','{':'}'}
        st = deque()
        for c in s:
            if c not in parens and (not st or parens[st.pop()]!=c):
                return False
            elif c in parens:
                st.append(c)
        return len(st)==0
```
# How it works
I create a hash map mapping the parentheses to each other to avoid having a massive if else statement, then create a stack for my parentheses. I iterate through the string, adding open parentheses to the queue, and on closed parentheses
I pop from the queue. If they are a matching set, continue, if not or the stack is empty, return false. If after looping through the entire string the stack is empty, then all the parentheses pairs were valid and I return true.
# Runtime analysis
My implementation is `O(n)` where `n` is the length of the string `s`. Add to push and pop in a stack are both `O(1)` operations, and I perform one of these operations on each character in the string. I also lookup in the hashmap, but this is 
a constant operation since the length of the hash map is only 3
# Memory usage
My implementation uses `O(n)` extra space, since I create a stack that will hold at most `O(n/2)` items, which grows similarly to `O(n)` when scaling the input to arbitrarily large sizes.
