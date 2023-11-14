
  # longest-common-prefix

  ```c
  char* longestCommonPrefix(char** strs, int strsSize) {
    if (strsSize == 0) {
        return "";
    }

    int minLen = strlen(strs[0]);

    for (int i = 1; i < strsSize; i++) {
        int j = 0;
        while (strs[0][j] && strs[i][j] && strs[0][j] == strs[i][j]) {
            j++;
        }
        if (j < minLen) {
            minLen = j;
        }
    }

    char* result = (char*)malloc((minLen + 1) * sizeof(char));
    strncpy(result, strs[0], minLen);
    result[minLen] = '\0';

    return result;
}
  ```
  