## Lab 3: Remove Subfolders from the Filesystem
### Code
``` 
        // REAL REAL REAL SOLUTION
        // sort alphabetically, this will get them in order n stuff
        // this will get the shortest keys first naturally, so it will be /a before /a/b
        // examples: "/a/b", "/a/b/c/d", "/a/c", "/a/e", "/a/e/f"
        // because it's sorted like this, we only need to keep track of one "root"
        // the roots in this case are "/a/b", "/a/c", "/a/e" since they are not subfolders of "root" before
        // and if it's different from the original, we add it to an output list (easy enough)
        // so basically, we save 1 string of the root. we then compare every object after
        // the isseu ith using a string is that what if it's like "/a/b/c" and the root is "b/c"
        // AFTER RESEARCH: can use "startsWith" function, which means this is fine to use 
        // the  contains each 'folder' in order
        // TO COMPARE
        // we compare this string to each element of the next in the string
        // if it srtarts with something differemt, then that's bad, its not a subfolder
        // we break and make that the new root, and add it to output
        // if it's not differet, oh well!!! just keep going 

class Solution {
    public List<String> removeSubfolders(String[] folder) {

        // sort alphabetically, hint was given in recitation, makes it so all roots come first
        Arrays.sort(folder); // use collections sort, this is O(n log n) i think
        
        List<String> resultList = new ArrayList<>(); // submit an array list
        
        String root = ""; // this will be our root
        String currentFolder = ""; // this is thing we compare root to

        for (int i = 0; i < folder.length; i++) { // iterate through
            currentFolder = folder[i]; // get a golder
            if (root.isEmpty() || !currentFolder.startsWith(root + "/")) { 
                // if the root is empty (aka, first element) or if current folder does NOT have the root before it 
                // (plus a slash, bc otherwise would be true for "a/b/ca" AND "a/b/c/a")
                resultList.add(currentFolder); // add this 
                root = currentFolder; // the current folder is the root #awesome 
            }
        }
        
        return resultList;
    }
}
```

### Code Explanation
My code sorts the list of folders alphabetically so that all of the higher keys will come first. It then iterates through the list of folders; if 
the folder is different from the root (or if the root is empty, like for folder[0]), then it will add to a list of unique folders. If the folder is 
the same, the loop will just continue, as we don't need to do anything special with subfolders. I think the most important part of the code is the
'startsWith' function, something I didn't know existed until I tried to implement it myself. This allows using a string rather than a linked list, which I
will talk about in a second. The reason it is difficult to use a string without it is because the program has to differentiate between "/a/b/" and "/d/a/b"
for example. Using just .contains, the program would assume the root of "/a/b" would have a subfolder of "/d/a/b", which is not the case. 
Like last week, I went through many different iterations of code trying to find the best one to use. I had originally used a design that used linked lists 
and iterators, but I scrapped it halfway through because it had so many lines of code and was difficult to debug. While I think it might have ran a little 
faster, this solution is much easier to understand and debug. I kept all of my original comments in to help see my thought process.
### Time and Space Complexity
While my loop itself is only O(n), Collections.sort is O(n log n). Since nothing else in the program significantly contributes to runtime, my overall 
worst case runtime is O(n log n), where n is the number of strings in the folder array. For space complexity, I do create an entire separate ArrayList to
submit the rest of the roots, which means my space complexity is worst case O(n), where n is the number of strings in the folder array. The problem specified 
that the length of folder names has to be less than 100 characters, so since I know that I am assuming comparing strings takes O(1) time.
