
  # calculate-digit-sum-of-a-string

  ```javascript
  /**
 * @param {string} s
 * @param {number} k
 * @return {string}
 */
var digitSum = function(s, k) {
    while (s.length > k) {
        let news = "";
        s.match(RegExp(`.{1,${k}}`, "g")).forEach(slice => {

            news += slice
                .split("")
                .map(elem => parseInt(elem))
                .reduce((acc, curr) => acc + curr);
            
        });
        s = news;
    }
    return s;
};
  ```
  