
  # minimum-window-substring

  ```javascript
  /**
 * @param {string} s
 * @param {string} t
 * @return {string}
 */
function minWindow(s, t) {
  // Create a character map for string t
  const tMap = {};
  for (let char of t) {
    tMap[char] = (tMap[char] || 0) + 1;
  }

  let left = 0;
  let count = Object.keys(tMap).length;
  let minLength = Infinity;
  let minWindowStart = 0;

  for (let right = 0; right < s.length; right++) {
    const char = s[right];

    if (char in tMap) {
      tMap[char]--;
      if (tMap[char] === 0) count--;
    }

    while (count === 0) {
      if (right - left + 1 < minLength) {
        minLength = right - left + 1;
        minWindowStart = left;
      }

      const leftChar = s[left];
      if (leftChar in tMap) {
        tMap[leftChar]++;
        if (tMap[leftChar] > 0) count++;
      }

      left++;
    }
  }

  if (minLength === Infinity) return "";
  return s.substr(minWindowStart, minLength);
}

  ```
  