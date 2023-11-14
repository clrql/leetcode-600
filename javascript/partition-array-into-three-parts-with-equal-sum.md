
  # partition-array-into-three-parts-with-equal-sum

  ```javascript
  /**
 * @param {number[]} arr
 * @return {boolean}
 */
var canThreePartsEqualSum = function(arr) {
    const sum = arr.reduce((a,b) => a+b); // Suma de todo
    if (sum % 3) return false; // Si la suman de todo no es divisible entre 3 retorna false

    const target = sum / 3; // Cuanto debe sumar cada parte
    let partSum = 0, count = 0;

    for  (let i = 0; i < arr.length; i++) {
        partSum += arr[i]
        if (partSum === target) {
            count++;
            partSum = 0;
        }
    }

    return count >= 3;
};
  ```
  