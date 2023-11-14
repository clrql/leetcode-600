
  # combination-sum-ii

  ```javascript
  /**
 * @param {number[]} candidates
 * @param {number} target
 * @return {number[][]}
 */
var combinationSum2 = function(candidates, target) {
    const result = [];
    const uniqueCombinations = new Set();

    candidates.sort((a, b) => a - b); // Sort the candidates in ascending order.

    const dfs = (start, current, currentSum) => {
        if (currentSum === target) {
            uniqueCombinations.add([...current]);
            return;
        }

        if (currentSum > target || start === candidates.length) {
            return;
        }

        for (let i = start; i < candidates.length; i++) {
            // Skip duplicates to avoid duplicate combinations.
            if (i > start && candidates[i] === candidates[i - 1]) {
                continue;
            }

            current.push(candidates[i]);
            dfs(i + 1, current, currentSum + candidates[i]);
            current.pop();
        }
    };

    dfs(0, [], 0);

    return Array.from(uniqueCombinations);
};
  ```
  