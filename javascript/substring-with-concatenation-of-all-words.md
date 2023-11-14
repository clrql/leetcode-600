
  # substring-with-concatenation-of-all-words

  ```javascript
  /**
 * @param {string} s
 * @param {string[]} words
 * @return {number[]}
 */
function findSubstring(s, words) {
  const result = [];
  if (s.length === 0 || words.length === 0) {
    return result;
  }
  
  const wordLength = words[0].length;
  const wordCount = words.length;
  const totalLength = wordLength * wordCount;
  
  const wordMap = {};
  for (const word of words) {
    if (wordMap[word]) {
      wordMap[word]++;
    } else {
      wordMap[word] = 1;
    }
  }
  
  for (let i = 0; i <= s.length - totalLength; i++) {
    const substring = s.substr(i, totalLength);
    const substringMap = {};
    
    for (let j = 0; j < totalLength; j += wordLength) {
      const word = substring.substr(j, wordLength);
      if (wordMap[word]) {
        if (substringMap[word]) {
          substringMap[word]++;
        } else {
          substringMap[word] = 1;
        }
        
        if (substringMap[word] > wordMap[word]) {
          break;
        }
      } else {
        break;
      }
    }
    
    if (compareMaps(wordMap, substringMap)) {
      result.push(i);
    }
  }
  
  return result;
}

function compareMaps(map1, map2) {
  for (const key in map1) {
    if (map1[key] !== map2[key]) {
      return false;
    }
  }
  
  return true;
}

  ```
  