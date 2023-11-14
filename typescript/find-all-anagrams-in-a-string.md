
  # find-all-anagrams-in-a-string

  ```typescript
  function findAnagrams(s: string, p: string): number[] {
    const result: number[] = [];
    const pMap = new Map<string, number>();
    let windowStart = 0;
    let matched = 0;

    // Create a frequency map of characters in string p
    for (const char of p) {
        pMap.set(char, (pMap.get(char) || 0) + 1);
    }

    // Slide the window over string s
    for (let windowEnd = 0; windowEnd < s.length; windowEnd++) {
        const rightChar = s[windowEnd];

        // Decrement the frequency of the character going out of the window
        if (pMap.has(rightChar)) {
        pMap.set(rightChar, pMap.get(rightChar)! - 1);
        if (pMap.get(rightChar) === 0) {
            matched++;
        }
        }

        // If all characters are matched, add the window start index to the result
        if (matched === pMap.size) {
        result.push(windowStart);
        }

        // Slide the window by one character
        if (windowEnd >= p.length - 1) {
        const leftChar = s[windowStart];
        windowStart++;

        // Increment the frequency of the character going into the window
        if (pMap.has(leftChar)) {
            if (pMap.get(leftChar) === 0) {
            matched--;
            }
            pMap.set(leftChar, pMap.get(leftChar)! + 1);
        }
        }
    }

    return result;
}

  ```
  