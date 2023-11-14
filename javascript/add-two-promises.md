
  # add-two-promises

  ```javascript
  /**
 * @param {Promise} promise1
 * @param {Promise} promise2
 * @return {Promise}
 */
var addTwoPromises = async function(promise1, promise2) {
    return new Promise((resolve) => {
        let cnt = 2, res = 0;
        const handler = (n) => {
            res += n, cnt--;
            if (!cnt) resolve(res)
        }
        promise1.then(handler)
        promise2.then(handler)
    })
};

/**
 * addTwoPromises(Promise.resolve(2), Promise.resolve(2))
 *   .then(console.log); // 4
 */
  ```
  