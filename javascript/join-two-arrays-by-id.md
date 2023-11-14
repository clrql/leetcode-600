
  # join-two-arrays-by-id

  ```javascript
  /**
 * @param {Array} arr1
 * @param {Array} arr2
 * @return {Array}
 */
var join = function(arr1, arr2) {
  var mergedMap = {};

  // Merge objects from arr1
  for (var i = 0; i < arr1.length; i++) {
    var obj = arr1[i];
    var id = obj.id;
    mergedMap[id] = obj;
  }

  // Merge objects from arr2
  for (var j = 0; j < arr2.length; j++) {
    var obj = arr2[j];
    var id = obj.id;
    if (mergedMap[id]) {
      // Merge properties
      for (var prop in obj) {
        mergedMap[id][prop] = obj[prop];
      }
    } else {
      mergedMap[id] = obj;
    }
  }

  // Convert mergedMap values to array
  var joinedArray = Object.values(mergedMap);

  // Sort array by id in ascending order
  joinedArray.sort(function(a, b) {
    return a.id - b.id;
  });

  return joinedArray;
};
  ```
  