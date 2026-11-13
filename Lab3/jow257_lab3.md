# My implementation
```
class Solution:
    def removeSubfolders(self, folder: list[str]) -> list[str]:
        folder.sort()
        superFolder=folder[0]
        superfolders=[superFolder]
        for i in range(1,len(folder)):
            if not (superFolder in folder[i] and folder[i][len(superFolder)]=='/' and folder[i].index(superFolder)==0):
                superFolder=folder[i]
                superfolders.append(superFolder)
        return superfolders
```
# What is going on and why it works.
The general idea is that we keep track of each super folder, and if the following folders are in the super folder, remove them from the folder. I do this by first sorting the folders, and by the nature of sorting, this makes it so that 
the superfolder will come directly before all of the subfolders that it contains. Then, we save the first folder as a superfolder, and check the following folders to see if they are subfolders of that superfolder. Once a folder is not a subfolder 
of the superfolder, it becomes a superfolder for the following subfolders. We keep track of every superfolder, and return them all at the end.

# Runtime and memory analysis
### Runtime
The runtime of my implementation would be `O(nlog(n))` because it sorts the given array, which is known to be an `O(nlog(n))`. After sorting, my code iterates through the array once, performing a constant amount of work on each string, which is 
`O(n)`. `O(nlog(n)) + O(n) = O(nlog(n))`.
### Memory
The memory cost of my implementation would be `O(n)`. Sorting with quicksort is `O(n)`, and I also create a new array which would contain `O(n)` items in the worst case. Therefore, my implementation is `O(n)`, since `O(n)+O(n)=O(n)`.
