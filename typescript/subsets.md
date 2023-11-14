
  # subsets

  ```typescript
  function subsets(nums: number[]): number[][] {
    const subsets: number[][] = [];
    
    backtrack([], 0);

    function backtrack(currentSubset: number[], start: number) {
        subsets.push([... currentSubset]);
        for (let i = start; i < nums.length; i++) {
            currentSubset.push(nums[i]);
            backtrack(currentSubset, i+1);
            currentSubset.pop()
        }
    }

    return subsets;
};


  ```
  