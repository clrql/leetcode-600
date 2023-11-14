
  # teemo-attacking

  ```javascript
  /**
 * @param {number[]} timeSeries
 * @param {number} duration
 * @return {number}
 */
var findPoisonedDuration = function(timeSeries, duration) {
  var totalDuration = 0;
  var n = timeSeries.length;

  for (var i = 0; i < n; i++) {
    if (i > 0 && timeSeries[i] < timeSeries[i - 1] + duration) {
      totalDuration += timeSeries[i] - timeSeries[i - 1];
    } else {
      totalDuration += duration;
    }
  }

  return totalDuration;
};

  ```
  