
  # day-of-the-year

  ```javascript
  /**
 * @param {string} date
 * @return {number}
 */
var dayOfYear = function(date) {
    date = date.split("-");
    let 
    year  = parseInt(date[0]),
    month = parseInt(date[1]),
    day   = parseInt(date[2]);

    let days = [
        0,
        31,
        28,
        31,
        30,
        31,
        30,
        31,
        31,
        30,
        31,
        30,
        31
    ]

    if (
        !(year % 4) &&
        !!(year % 100) ||
        !(year % 400)
    ) days[2] = 29;

    let total = 0;
    for (let i = 1; i <= month - 1; i++) {
        total += days[i];
    }

    total += day;

    return total;
};
  ```
  