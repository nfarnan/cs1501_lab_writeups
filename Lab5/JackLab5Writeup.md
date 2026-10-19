## Lab 5: LZW with Variable Width Codewords 
### Code
``` 
public class LZW {
    private static final int R = 256; // number of input chars
    private static int L = 512; // number of codewords = 2^W      !
    private static int W = 9; // codeword width                   !

    public static void compress() {
        W = 9;                                                  //!
        L = 512;                                                //!
        String input = BinaryStdIn.readString();
        TST<Integer> st = new TST<Integer>();
        for (int i = 0; i < R; i++)
            st.put("" + (char) i, i);
        int code = R + 1; // R is codeword for EOF

        while (input.length() > 0) {
            String s = st.longestPrefixOf(input); // Find max prefix match s.
            BinaryStdOut.write(st.get(s), W); // Print s's encoding.
            int t = s.length();
            if (W < 16 && code >= L) {                          //!
                W++; // increase bit size                       //!
                L = (int) Math.pow(2, (double) W);              //!
            }                                                   //!
            if (t < input.length() && code < L) // ! Add s to symbol table.
                st.put(input.substring(0, t + 1), code++);
            input = input.substring(t); // Scan past s in input.
        }
        BinaryStdOut.write(R, W);
        BinaryStdOut.close();
    }

    public static void expand() {
        String[] st = new String[65536];                        //!
        int i; // next available codeword value
        L = 512;                                                //!
        W = 9;                                                  //!
        // initialize symbol table with all 1-character strings
        for (i = 0; i < R; i++)
            st[i] = "" + (char) i;
        st[i++] = ""; // (unused) lookahead for EOF

        int codeword = BinaryStdIn.readInt(W);
        if (codeword == R)
            return; // expanded message is empty string
        String val = st[codeword];

        while (true) {
            BinaryStdOut.write(val);
            codeword = BinaryStdIn.readInt(W);
            if (codeword == R)
                break;
            String s = st[codeword];
            if (i == codeword)
                s = val + val.charAt(0); // special case hack
            if (i < L)
                st[i++] = val + s.charAt(0);
            if (W < 16 && i >= L) {                            //!
                W++;                                           //!
                L = (int) Math.pow(2, (double) W);             //!
            }                                                  //!
            val = s;
        }
        BinaryStdOut.close();
    }
}

```

### Code Explanation
I have marked all the lines I changed with an '!' comment. I first changed the L and W variables to be the starting amount (512 codewords, size of 9).
For compression, I implemented a check that increases the codeword width whenever the codebook fills up as long as the codeword is less than 16 chars.
I also adjust the codebook size to be 2^W. For expansion, I implemented a similar check in which if the current index is further than the length of 
a codebook of 2^W entries, the codeword width as well as the codebook size increases. Like the other check, it only does this if W is less than 16.

### Time and Space Complexity
My code does not add any significant time/space complexity differences. I believe that LZW compression is O(n) time and space xcomplexity normally, an
d from what I can see, the code reflects that. Since I did not change the substring calls, there is a chance it is a larger time complexity than O(n). 
So, both time and space complexity are O(n).
