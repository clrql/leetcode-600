
  # minimum-size-subarray-sum

  ```javascript
  /**
 * @param {number} target
 * @param {number[]} nums
 * @return {number}
 */
function minSubArrayLen(target, nums) {
  let minLength = Infinity;
  const prefixSum = [0];

  for (let i = 1; i <= nums.length; i++) {
    prefixSum[i] = prefixSum[i - 1] + nums[i - 1];
  }

  for (let i = 0; i < prefixSum.length; i++) {
    const end = binarySearch(prefixSum, i + 1, prefixSum.length - 1, prefixSum[i] + target);
    if (end !== -1) {
      minLength = Math.min(minLength, end - i);
    }
  }

  return minLength !== Infinity ? minLength : 0;
}

function binarySearch(nums, left, right, target) {
  while (left <= right) {
    const mid = Math.floor((left + right) / 2);
    if (nums[mid] === target) {
      return mid;
    } else if (nums[mid] < target) {
      left = mid + 1;
    } else {
      right = mid - 1;
    }
  }

  return left >= nums.length ? -1 : left;
}
  ```
  