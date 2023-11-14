
  # relative-ranks

  ```javascript
  /**
 * @param {number[]} score
 * @return {string[]}
 */
var findRelativeRanks = function(score) {
  var sortedScore = [...score].sort((a, b) => b - a);
  var rankMap = new Map();

  for (var i = 0; i < sortedScore.length; i++) {
    if (i === 0) {
      rankMap.set(sortedScore[i], "Gold Medal");
    } else if (i === 1) {
      rankMap.set(sortedScore[i], "Silver Medal");
    } else if (i === 2) {
      rankMap.set(sortedScore[i], "Bronze Medal");
    } else {
      rankMap.set(sortedScore[i], (i + 1).toString());
    }
  }

  var result = [];
  for (var j = 0; j < score.length; j++) {
    result.push(rankMap.get(score[j]));
  }

  return result;
};

  ```
  