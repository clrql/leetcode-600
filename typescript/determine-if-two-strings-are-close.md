
  # determine-if-two-strings-are-close

  ```typescript
  function closeStrings(word1: string, word2: string): boolean {
  if (word1.length !== word2.length) {
    return false;
  }

  const count1 = new Map<string, number>();
  const count2 = new Map<string, number>();
  const chars1 = new Set<string>();
  const chars2 = new Set<string>();

  for (const char of word1) {
    count1.set(char, (count1.get(char) || 0) + 1);
    chars1.add(char);
  }

  for (const char of word2) {
    count2.set(char, (count2.get(char) || 0) + 1);
    chars2.add(char);
  }

  const counts1 = Array.from(count1.values()).sort((a, b) => a - b);
  const counts2 = Array.from(count2.values()).sort((a, b) => a - b);

  const chars1Array = Array.from(chars1);
  const chars2Array = Array.from(chars2);

  chars1Array.sort();
  chars2Array.sort();

  return arraysEqual(counts1, counts2) && arraysEqual(chars1Array, chars2Array);
}

function arraysEqual<T>(arr1: T[], arr2: T[]): boolean {
  if (arr1.length !== arr2.length) {
    return false;
  }

  for (let i = 0; i < arr1.length; i++) {
    if (arr1[i] !== arr2[i]) {
      return false;
    }
  }

  return true;
}

  ```
  