
  # is-object-empty

  ```javascript
  /**
 * @param {Object | Array} obj
 * @return {boolean}
 */
var isEmpty = function(obj) {
    return ["[]", "{}"].includes(JSON.stringify(obj))
};
  ```
  