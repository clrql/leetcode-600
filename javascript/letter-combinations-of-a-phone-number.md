
  # letter-combinations-of-a-phone-number

  ```javascript
  /**
 * @param {string} digits
 * @return {string[]}
 */
var letterCombinations = function(digits) {
    if (!digits) {
        return [];
    }
    const digitMap = {
        '2': ['a', 'b', 'c'],
        '3': ['d', 'e', 'f'],
        '4': ['g', 'h', 'i'],
        '5': ['j', 'k', 'l'],
        '6': ['m', 'n', 'o'],
        '7': ['p', 'q', 'r', 's'],
        '8': ['t', 'u', 'v'],
        '9': ['w', 'x', 'y', 'z'],
    }
    const result = [];
    const generateCombinations = function(combination, digits) {
        if (digits.length === 0) {
            return result.push(combination)
        } else {
            const letters = digitMap[digits.charAt(0)];
            for (let i = 0; i < letters.length; i++) {
                generateCombinations(combination+letters[i], digits.substring(1))
            }
        }
        
    }

    generateCombinations('', digits);

    return result
};
  ```
  