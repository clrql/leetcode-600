
  # x-of-a-kind-in-a-deck-of-cards

  ```javascript
  /**
 * @param {number[]} deck
 * @return {boolean}
 */
var hasGroupsSizeX = function(deck) {
    const counts = new Map();
    for (const card of deck) {
        if (counts.has(card)) {
            counts.set(card, counts.get(card) + 1);
        } else {
            counts.set(card, 1);
        }
    }

    const values = Array.from(counts.values());
    let gcd = values[0];
    for (let i = 1; i < values.length; i++) {
        gcd = GCD(gcd, values[i]);
    }

    return gcd >= 2;
};

function GCD(a, b) {
    if (b === 0) return a;
    return GCD(b, a % b);
}
  ```
  