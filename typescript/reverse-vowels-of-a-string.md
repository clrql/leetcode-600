
  # reverse-vowels-of-a-string

  ```typescript
  function reverseVowels(s: string): string {
    const vowels = ['a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U'];
    const arr = s.split('');
    let start = 0;
    let end = s.length - 1;

    while (start < end) {
        while (start < end && !vowels.includes(arr[start])) {
        start++;
        }

        while (start < end && !vowels.includes(arr[end])) {
        end--;
        }

        if (start < end) {
        const temp = arr[start];
        arr[start] = arr[end];
        arr[end] = temp;
        start++;
        end--;
        }
    }

    return arr.join('');
};
  ```
  