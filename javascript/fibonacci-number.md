
  # fibonacci-number

  ```javascript
  /**
 * @param {number} n
 * @return {number}
 */
var fib = function(n) {
    if(n < 2) return n;

    let next, prev = 0; curr = 1;
    for(let i = 2; i <= n; i++){
        next = prev + curr;
        prev = curr;
        curr = next;
    }
    return next;
};
  ```
  