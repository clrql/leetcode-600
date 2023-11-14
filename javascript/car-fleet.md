
  # car-fleet

  ```javascript
  /**
 * @param {number} target
 * @param {number[]} position
 * @param {number[]} speed
 * @return {number}
 */
var carFleet = function(target, position, speed) {
    const n = position.length;
    const cars = Array(n).fill().map((_, i) => ({ position: position[i], time: (target - position[i]) / speed[i] }));
    cars.sort((a, b) => b.position - a.position);
    let fleets = 0, prevTime = 0;
    for (let i = 0; i < n; i++) {
        if (cars[i].time > prevTime) {
            prevTime = cars[i].time;
            fleets++;
        }
    }
    return fleets;
};
  ```
  