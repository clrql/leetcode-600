
  # sliding-window-maximum

  ```typescript
  function maxSlidingWindow(nums: number[], k: number): number[] {
    const result: number[] = [];
    const deque: number[] = [];

    for (let i = 0; i < nums.length; i++) {
        // Remove elements from the front of the deque that are outside the current window
        if (deque.length > 0 && deque[0] <= i - k) {
        deque.shift();
        }

        // Remove elements from the back of the deque that are smaller than the current element
        while (deque.length > 0 && nums[deque[deque.length - 1]] < nums[i]) {
        deque.pop();
        }

        deque.push(i);

        // Add the maximum element to the result when the window size is reached
        if (i >= k - 1) {
        result.push(nums[deque[0]]);
        }
    }

    return result;
}

  ```
  