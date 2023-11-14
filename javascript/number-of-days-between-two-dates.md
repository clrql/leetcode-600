
  # number-of-days-between-two-dates

  ```javascript
  /**
 * @param {string} date1
 * @param {string} date2
 * @return {number}
 */
var daysBetweenDates = function(date1, date2) {
    let startDate = new Date(date1);
    let endDate = new Date(date2);
    
    const diff = endDate - startDate;
    const days = Math.floor(diff / (1000*60*60*24));

    return Math.abs(days);
};
  ```
  