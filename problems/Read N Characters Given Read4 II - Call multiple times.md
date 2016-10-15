# Read N Characters Given Read4 II - Call multiple times

The API: `int read4(char *buf)` reads 4 characters at a time from a file.

The return value is the actual number of characters read. For example, it returns 3 if there is only 3 characters left in the file.

By using the `read4` API, implement the function `int read(char *buf, int n)` that reads n characters from the file.

**Note:**

The read function may be called multiple times.

**Solution:**
```java
/* The read4 API is defined in the parent class Reader4.
      int read4(char[] buf); */

public class Solution extends Reader4 {
  // a pointer in the buffer
  int ptr = 0;
  // how many left in the buffer after last call
  int left = 0;
  // as read() can be called multiple times
  // we should only allocate the buffer once
  char[] buffer = new char[4];

  /**
   * @param buf Destination buffer
   * @param n   Maximum number of characters to read
   * @return    The number of characters read
   */
  public int read(char[] buf, int n) {
    // end of file flag
    boolean eof = false;
    // total bytes have been read this time
    int total = 0;

    while (!eof && total < n) {
      // if we still have some leftovers, use them
      // otherwise we read another 4 chars
      int size  = (left > 0) ? left : read4(buffer);

      // check if it's the end of the file
      eof = (left == 0 && size < 4);

      // get the actual count we are going to read
      int count = Math.min(size, n - total);

      // update the count of leftovers
      left = size - count;

      // copy
      for (int i = 0; i < count; i++)
        buf[total++] = buffer[ptr + i];

      // update the pointer
      ptr = (ptr + count) % 4;
    }

    return total;
  }
}
```