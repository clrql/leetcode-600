
  # sort-the-people

  ```javascript
  /**
 * @param {string[]} names
 * @param {number[]} heights
 * @return {string[]}
 */
var sortPeople = function(names, heights) {
    let heightEntries = {};
    heights.forEach((value, index) => {
        heightEntries[value] = index;
    })
    let sortedHeights = heights.sort((a,b)=>b-a)
    let sortedPeople = [];

    sortedHeights.forEach((val) => {
        sortedPeople.push(names[heightEntries[val]])
    })

    return sortedPeople
};
  ```
  