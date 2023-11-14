
  # convert-object-to-json-string

  ```javascript
  /**
 * @param {any} object
 * @return {string}
 */
var jsonStringify = function(object) {
    if (object === null) return "null";
    if (typeof object === "string") return '"' + object + '"';
    if (typeof object === "number" || typeof object === "boolean") {
        return object.toString();
    }
    if (Array.isArray(object)) {
        var arrResult = [];
        for (var i = 0; i < object.length; i++) {
            arrResult.push(jsonStringify(object[i]))
        }
        return "[" + arrResult.join(",") + "]";
    }
    var objResult = [];
    var keys = Object.keys(object);
    for (var i = 0; i < keys.length; i++) {
        var key = keys[i];
        var val = jsonStringify(object[key]);
        objResult.push('"' + key + '":' + val);
    }
    return "{" + objResult.join(",") + "}";
};
  ```
  