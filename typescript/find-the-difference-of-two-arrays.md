
  # find-the-difference-of-two-arrays

  ```typescript
  function findDifference(nums1: number[], nums2: number[]): number[][] {
  const set1 = new Set(nums1);
  const set2 = new Set(nums2);

  const answer: number[][] = [];

  const distinctNums1: number[] = [];
  const distinctNums2: number[] = [];

  for (const num of set1) {
    if (!set2.has(num)) {
      distinctNums1.push(num);
    }
  }

  for (const num of set2) {
    if (!set1.has(num)) {
      distinctNums2.push(num);
    }
  }

  answer.push(distinctNums1);
  answer.push(distinctNums2);

  return answer;
}

  ```
  