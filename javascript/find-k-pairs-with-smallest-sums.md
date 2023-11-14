
  # find-k-pairs-with-smallest-sums

  ```javascript
  /**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @param {number} k
 * @return {number[][]}
 */
var kSmallestPairs = function(nums1, nums2, k) {
    
    if (nums1.length === 0 || nums2.length === 0) return []
    
    let arr = [];
    let max = -Infinity;
    
    for (let i = 0; i < nums1.length; i++) {
        for (let j = 0; j < nums2.length; j++) {

            let obj = {
                sum: nums1[i] + nums2[j],
                nums: [nums1[i], nums2[j]]
            }
            
            if (obj.sum >= max && arr.length >= k) {
                break;
            } else if (obj.sum <= max && arr.length < k) {
                arr.push(obj);
            } else if (obj.sum > max && arr.length < k) {
                max = obj.sum; 
                arr.push(obj);
            } else if (obj.sum < max && arr.length >= k) {
                let newMax = -Infinity;
                let replaced = false;
                for (let n = 0; n < arr.length; n++) {
                    if (!replaced && arr[n].sum === max) {
                        arr[n] = obj;
                        replaced = true;
                    }
                    if (arr[n].sum > newMax) newMax = arr[n].sum
                }
                max = newMax;
            } 
        }
    }
    
    return arr.map(obj => obj.nums);
    
};
  ```
  