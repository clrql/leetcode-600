
  # zigzag-conversion

  ```typescript
  function convert(s: string, numRows: number): string {
    if (numRows === 1 || s.length <= numRows) {
        return s;
    }

    const resultRows: string[] = new Array(numRows).fill('');
    let currentRow = 0;
    let direction = -1;

    for (let i = 0; i < s.length; i++) {
        resultRows[currentRow] += s[i];

        if (currentRow === 0 || currentRow === numRows - 1) {
            direction *= -1;
        }

        currentRow += direction;
    }

    return resultRows.join('');
};
  ```
  