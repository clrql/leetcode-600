
  # execute-asynchronous-functions-in-parallel

  ```javascript
  /**
 * @param {Array<Function>} functions
 * @return {Promise<any>}
 */
var promiseAll = async function(functions) {
  return new Promise((resolve, reject) => {
    let ans = [];
    let j = functions.length;
    functions.forEach((func, i) => {
      func()
      .then(r => (ans[i] = r, --j == 0 && resolve(ans)))
      .catch(reject)
    })
  })
};



/**
 * const promise = promiseAll([() => new Promise(res => res(42))])
 * promise.then(console.log); // [42]
 */
  ```
  