
  # counting-bits

  ```typescript
  function countBits(n: number): number[] {
    let ans: number[] = new Array(n+1).fill(0);

    for (let i = 0; i <= n; i++) {
        ans[i] = i.toString(2).replace(/0/g, "").length;
    }

    return ans;
};
  ```
  