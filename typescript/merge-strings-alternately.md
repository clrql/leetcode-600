
  # merge-strings-alternately

  ```typescript
  function mergeAlternately(word1: string, word2: string): string {
    let merged = '';
    const length = Math.max(word1.length, word2.length);

    for (let i = 0; i < length; i++) {
        if (i < word1.length) {
        merged += word1[i];
        }
        if (i < word2.length) {
        merged += word2[i];
        }
    }

    return merged;
};
  ```
  