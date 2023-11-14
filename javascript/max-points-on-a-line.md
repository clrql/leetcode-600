
  # max-points-on-a-line

  ```javascript
  /**
 * @param {number[][]} points
 * @return {number}
 */
var maxPoints = function(points) {
    if (points.length <= 2) {
        return points.length;
    }
    
    let maxCount = 0;
    
    for (let i = 0; i < points.length; i++) {
        const slopes = {};
        let duplicatePoints = 0;
        let currentMax = 0;
        
        for (let j = i + 1; j < points.length; j++) {
            const x1 = points[i][0];
            const y1 = points[i][1];
            const x2 = points[j][0];
            const y2 = points[j][1];
            
            if (x1 === x2 && y1 === y2) {
                duplicatePoints++;
            } else {
                const slope = (x1 - x2) === 0 ? Infinity : (y1 - y2) / (x1 - x2);
                slopes[slope] = (slopes[slope] || 0) + 1;
                currentMax = Math.max(currentMax, slopes[slope]);
            }
        }
        
        maxCount = Math.max(maxCount, currentMax + duplicatePoints + 1);
    }
    
    return maxCount;
};
  ```
  