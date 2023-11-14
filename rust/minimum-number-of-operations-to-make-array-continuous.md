
  # minimum-number-of-operations-to-make-array-continuous

  ```rust
  impl Solution {
    pub fn min_operations(nums: Vec<i32>) -> i32 {
        let mut nums = nums;
        let n = nums.len();
        let mut ans = n as i32;
        nums.sort_unstable();
        nums.dedup();
        let m = nums.len();
        let mut j = 0;
        for i in 0..m {
            while j < m && nums[j] < nums[i] + n as i32 {
                j += 1;
            }
            ans = ans.min(n as i32 - j as i32 + i as i32);
        }
        ans
    }
}
  ```
  