
  # combination-sum-iii

  ```typescript
  function combinationSum3(k: number, n: number): number[][] {
  const combinations: number[][] = [];
  
  function backtrack(start: number, sum: number, combination: number[]): void {
    if (sum === n && combination.length === k) {
      combinations.push([...combination]);
      return;
    }
    
    if (sum > n || combination.length > k) {
      return;
    }
    
    for (let i = start; i <= 9; i++) {
      combination.push(i);
      backtrack(i + 1, sum + i, combination);
      combination.pop();
    }
  }
  
  backtrack(1, 0, []);
  return combinations;
}

  ```
  