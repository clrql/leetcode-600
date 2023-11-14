
  # single-number-ii

  ```javascript
  /**
 * @param {number[]} nums
 * @return {number}
 */
var singleNumber = function(nums) {
    //return nums.reduce((acc, curr) => acc ^= curr)
    nums.sort((a,b) => b-a);

    for (let i = 0; i < nums.length; i+=3) {
        if (nums[i] == nums[i+1]) {
            continue;
        } else {
            return nums[i]
        }
    }
    
};

/*
nums = 0,100,0,99,100,0,100
nums.sort(); // nums = 0,0,0,99,100,100,100

nums[i] == nums[i+1] {
    continue;
} else {
    return nums[i]
}


*/
  ```
  