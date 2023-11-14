
  # find-the-index-of-the-first-occurrence-in-a-string

  ```c
  int strStr(char* haystack, char* needle) {
    int haystackLen = strlen(haystack);
    int needleLen = strlen(needle);

    if (needleLen == 0) {
        return 0; // Needle is an empty string, it's always found at index 0.
    }

    if (haystackLen < needleLen) {
        return -1; // Needle is longer than haystack, it can't be found.
    }

    for (int i = 0; i <= haystackLen - needleLen; i++) {
        int j;
        for (j = 0; j < needleLen; j++) {
            if (haystack[i + j] != needle[j]) {
                break; // If characters don't match, break the inner loop.
            }
        }
        if (j == needleLen) {
            return i; // All characters matched, found a match.
        }
    }

    return -1; // No match found.
}

  ```
  