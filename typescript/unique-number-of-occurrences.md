
  # unique-number-of-occurrences

  ```typescript
  function uniqueOccurrences(arr: number[]): boolean {
  const occurrenceCount = new Map<number, number>();

  for (const num of arr) {
    if (occurrenceCount.has(num)) {
      occurrenceCount.set(num, occurrenceCount.get(num)! + 1);
    } else {
      occurrenceCount.set(num, 1);
    }
  }

  const occurrenceSet = new Set(occurrenceCount.values());

  return occurrenceSet.size === occurrenceCount.size;
}

  ```
  