
  # reverse-words-in-a-string

  ```typescript
  function reverseWords(s: string): string {
    // Trim leading and trailing spaces
    s = s.trim();

    // Split the string into an array of words
    const words = s.split(/\s+/);

    // Reverse the array of words
    const reversedWords = words.reverse();

    // Join the reversed words with a single space
    const reversedString = reversedWords.join(' ');

    return reversedString;
};
  ```
  