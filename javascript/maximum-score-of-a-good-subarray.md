
  # maximum-score-of-a-good-subarray

  ```javascript
  /**
 * @param {number[]} nums
 * @param {number} k
 * @return {number}
 */
var maximumScore = function(nums, k) {
    const n = nums.length;
    let maxScore = 0;
    const left = Array(n);
    const right = Array(n);

    // Calculate the first smaller element on the left of each element.
    const stack = [];
    for (let i = 0; i < n; i++) {
        while (stack.length > 0 && nums[stack[stack.length - 1]] >= nums[i]) {
            stack.pop();
        }
        left[i] = stack.length === 0 ? -1 : stack[stack.length - 1];
        stack.push(i);
    }

    // Clear the stack and calculate the first smaller element on the right.
    stack.length = 0;
    for (let i = n - 1; i >= 0; i--) {
        while (stack.length > 0 && nums[stack[stack.length - 1]] >= nums[i]) {
            stack.pop();
        }
        right[i] = stack.length === 0 ? n : stack[stack.length - 1];
        stack.push(i);
    }

    // Calculate the maximum score for each possible k.
    for (let i = 0; i < n; i++) {
        if (left[i] < k && right[i] > k) {
            maxScore = Math.max(maxScore, nums[i] * (right[i] - left[i] - 1));
        }
    }

    return maxScore;
};
  ```
  