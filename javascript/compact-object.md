
  # compact-object

  ```javascript
  /**
 * @param {Object} obj
 * @return {Object}
 */
var compactObject = function(obj) {
  if (Array.isArray(obj)) {
    return obj
      .filter(Boolean)
      .map(compactObject);
  }

  if (typeof obj === 'object' && obj !== null) {
    return Object.entries(obj)
      .reduce((acc, [key, value]) => {
        if (Boolean(value)) {
          acc[key] = compactObject(value);
        }
        return acc;
      }, {});
  }

  return obj;
};
  ```
  