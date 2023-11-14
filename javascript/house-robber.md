
  # house-robber

  ```javascript
  /**
 * @param {number[]} nums
 * @return {number}
 */
var rob = function(nums) {
    switch(nums.length) {
        case 0: return 0;
        case 1: return nums[0];
        case 2: return Math.max(nums[0], nums[1]);
    }

    const dp = [];
    dp[0] = nums[0];
    dp[1] = Math.max(nums[0], nums[1]);

    for (let i = 2; i < nums.length; i ++) {
        dp[i] = Math.max(dp[i-2] + nums[i], dp[i-1])
    }

    return dp[dp.length-1]
};
  ```
  