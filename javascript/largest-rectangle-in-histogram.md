
  # largest-rectangle-in-histogram

  ```javascript
  /**
 * @param {number[]} heights
 * @return {number}
 */
var largestRectangleArea = function(heights) {
    const stack = []; // Used to store the indices of the histogram bars
  let maxArea = 0;
  
  // Iterate through each bar in the histogram
  for (let i = 0; i <= heights.length; i++) {
    // Check if the current bar is shorter than the previous bar in the stack
    // Calculate the area of the rectangle formed by the previous bar
    while (stack.length > 0 && (i === heights.length || heights[i] < heights[stack[stack.length - 1]])) {
      const height = heights[stack.pop()]; // Pop the previous bar's index from the stack
      const width = stack.length === 0 ? i : i - stack[stack.length - 1] - 1;
      const area = height * width;
      maxArea = Math.max(maxArea, area);
    }
    
    stack.push(i); // Push the current bar's index into the stack
  }
  
  return maxArea;
};



/**
 * Returns indexes where target appeared
 * @param {number[]} arr
 * @param {number} target
 * @return {number[]} 
*/
const indexesOf = function(arr, target) {
    let indexes = [];
    for (let i = 0; i<arr.length; i++) {
        if (arr[i] == target) {
            indexes.push(i)
        }
    }
    return indexes;
}

/**
 * Returns the biggest number in a number array
 * In this case the tallest height
 * @param {number[]} arr
 * @return {number}
*/
const tallestOf = function(arr) {
    let max = -1;
    for (let i = 0; i < arr.length; i++) {
        if (arr[i] > max) {
            max = arr[i]
        }
    }
    return max;
}
  ```
  