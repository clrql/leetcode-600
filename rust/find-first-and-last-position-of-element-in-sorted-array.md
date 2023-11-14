
  # find-first-and-last-position-of-element-in-sorted-array

  ```rust
  impl Solution {
    pub fn search_range(nums: Vec<i32>, target: i32) -> Vec<i32> {
        let mut result = vec![-1, -1];
        if nums.is_empty() {
            return result;
        }

        let first_occurrence = Solution::find_first_occurrence(&nums, target);
        if first_occurrence == -1 {
            return result;
        }

        let last_occurrence = Solution::find_last_occurrence(&nums, target);
        result[0] = first_occurrence;
        result[1] = last_occurrence;
        result
    }

    fn find_first_occurrence(nums: &Vec<i32>, target: i32) -> i32 {
        let mut left = 0;
        let mut right = nums.len() as i32 - 1;
        let mut first_occurrence = -1;

        while left <= right {
            let mid = left + (right - left) / 2;
            if nums[mid as usize] == target {
                first_occurrence = mid;
                right = mid - 1;
            } else if nums[mid as usize] < target {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }

        first_occurrence
    }

    fn find_last_occurrence(nums: &Vec<i32>, target: i32) -> i32 {
        let mut left = 0;
        let mut right = nums.len() as i32 - 1;
        let mut last_occurrence = -1;

        while left <= right {
            let mid = left + (right - left) / 2;
            if nums[mid as usize] == target {
                last_occurrence = mid;
                left = mid + 1;
            } else if nums[mid as usize] < target {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }

        last_occurrence
    }
}

  ```
  