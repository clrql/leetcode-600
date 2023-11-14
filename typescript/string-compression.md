
  # string-compression

  ```typescript
  function compress(chars: string[]): number {
  let writeIdx = 0; // Index to write compressed characters
  let count = 1; // Count of consecutive repeating characters

  for (let i = 0; i < chars.length; i++) {
    if (i + 1 === chars.length || chars[i] !== chars[i + 1]) {
      // Current character is different from the next one or it's the last character
      chars[writeIdx] = chars[i]; // Write the character at the current write index

      if (count > 1) {
        // There is a group of repeating characters
        const countChars = count.toString().split(''); // Split the count into individual digits

        for (const char of countChars) {
          chars[++writeIdx] = char; // Write each digit of the count
        }
      }

      writeIdx++; // Move the write index forward
      count = 1; // Reset the count for the next group
    } else {
      // Current character is the same as the next one
      count++; // Increment the count
    }
  }

  return writeIdx;
}

  ```
  