
  # is-subsequence

  ```typescript
  function isSubsequence(s: string, t: string): boolean {
  let sIndex = 0; // Index for string s
  let tIndex = 0; // Index for string t

  while (sIndex < s.length && tIndex < t.length) {
    if (s[sIndex] === t[tIndex]) {
      // Characters match, move to the next character in s
      sIndex++;
    }
    // Move to the next character in t
    tIndex++;
  }

  // Check if all characters in s have been matched
  return sIndex === s.length;
}

  ```
  