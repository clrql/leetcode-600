
  # maximum-number-of-vowels-in-a-substring-of-given-length

  ```typescript
  function maxVowels(s: string, k: number): number {
  const vowels = new Set(['a', 'e', 'i', 'o', 'u']); // Set of vowel letters
  let maxVowelCount = 0; // Maximum vowel count
  let vowelCount = 0; // Current vowel count

  // Count the vowels in the first window of length k
  for (let i = 0; i < k; i++) {
    if (vowels.has(s[i])) {
      vowelCount++;
    }
  }

  maxVowelCount = vowelCount; // Initialize the maximum vowel count

  // Slide the window through the string
  for (let i = k; i < s.length; i++) {
    if (vowels.has(s[i])) {
      vowelCount++; // Increment the vowel count for the current character
    }

    if (vowels.has(s[i - k])) {
      vowelCount--; // Decrement the vowel count for the character that goes out of the window
    }

    maxVowelCount = Math.max(maxVowelCount, vowelCount); // Update the maximum vowel count
  }

  return maxVowelCount; // Return the maximum vowel count
}

  ```
  