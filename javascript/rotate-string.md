
  # rotate-string

  ```javascript
  /**
 * @param {string} s
 * @param {string} goal
 * @return {boolean}
 */
var rotateString = function(s, goal) {
    
    for (let i = 0; i < s.length; i++) {
        s = s.split("");
        s.push(s.shift());
        s = s.join("");
        
        if (s == goal) return true;
    }

    return false;
};
  ```
  