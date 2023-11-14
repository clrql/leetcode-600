
  # majority-element-ii

  ```javascript
  /**
 * @param {number[]} nums
 * @return {number[]}
 */

/*
var majorityElement = function(nums) { 
    let hashmap = {};
    let answer = [];
    if (nums.length < 3) {
        return [... new Set(nums)];
    }
    for (let num of nums) {
        if (!hashmap[num]) {
            hashmap[num] = 1;
        } else {
            hashmap[num]++;
            if (hashmap[num] > nums.length/3 && !answer.includes(num)) {
                answer.push(num);
            }
        }
    }
    return answer;
};

*/
var majorityElement = function(nums) {
    let hash = new Map();
    for (const num of nums) {
        hash.set(num, (hash.get(num) || 0) + 1);
    }
    return Array.from(hash.keys()).filter(num => hash.get(num) > nums.length / 3);
}
  ```
  