
  # subarray-sum-equals-k

  ```typescript
  function subarraySum(nums: number[], k: number): number {
    let count = 0;
    let sum = 0;
    const map = new Map<number, number>();
    map.set(0, 1);

    for (let i = 0; i < nums.length; i++) {
        sum += nums[i];
        if (map.has(sum - k)) {
        count += map.get(sum - k)!;
        }
        if (map.has(sum)) {
        map.set(sum, map.get(sum)! + 1);
        } else {
        map.set(sum, 1);
        }
    }

    return count;
}

  ```
  