# 157 Read N Characters Given Read4

有很多十分复杂的判断

```text
"""
The read4 API is already defined for you.

    @param buf4, a list of characters
    @return an integer
    def read4(buf4):

# Below is an example of how the read4 API can be called.
file = File("abcdefghijk") # File is "abcdefghijk", initially file pointer (fp) points to 'a'
buf4 = [' '] * 4 # Create buffer with enough space to store characters
read4(buf4) # read4 returns 4. Now buf = ['a','b','c','d'], fp points to 'e'
read4(buf4) # read4 returns 4. Now buf = ['e','f','g','h'], fp points to 'i'
read4(buf4) # read4 returns 3. Now buf = ['i','j','k',...], fp points to end of file
"""

class Solution:
    def read(self, buf, n):
        """
        :type buf: Destination buffer (List[str])
        :type n: Number of characters to read (int)
        :rtype: The number of actual characters read (int)
        """
        time = n // 4 + 1
        count = 0
        for i in range(time):
            #init buf4 every iter, otherwise cause issue
            buf4 = ["" for _ in range(4)]
            read4(buf4)
            #print(buf4, i)
            for j in range(4):
                if buf4[j] != '' and 4*i + j < n:
                    buf[4*i + j] = buf4[j]
                    count += 1
        #print(buf)
        return count
```

