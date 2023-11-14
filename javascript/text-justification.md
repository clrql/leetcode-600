
  # text-justification

  ```javascript
  /**
 * @param {string[]} words
 * @param {number} maxWidth
 * @return {string[]}
 */
function fullJustify(words, maxWidth) {
    const result = [];
    let currentLine = [];
    let currentWidth = 0;

    for (let i = 0; i < words.length; i++) {
        const word = words[i];

        if (currentWidth + currentLine.length + word.length <= maxWidth) {
            // Add word to current line
            currentLine.push(word);
            currentWidth += word.length;
        } else {
            // Create a new line
            result.push(justifyLine(currentLine, maxWidth, false));
            currentLine = [word];
            currentWidth = word.length;
        }
    }

    // Justify the last line
    result.push(justifyLine(currentLine, maxWidth, true));

    return result;
}

function justifyLine(line, maxWidth, isLastLine) {
    const numWords = line.length;
    const totalWidth = line.reduce((acc, word) => acc + word.length, 0);
    const totalSpaces = maxWidth - totalWidth;

    if (numWords === 1 || isLastLine) {
        // Left-justify the line if it's the last line or has only one word
        return line.join(' ') + ' '.repeat(maxWidth - totalWidth - (numWords - 1));
    } else {
        const numGaps = numWords - 1;
        const spacesPerGap = Math.floor(totalSpaces / numGaps);
        const extraSpaces = totalSpaces % numGaps;

        let justifiedLine = '';
        for (let i = 0; i < line.length; i++) {
            justifiedLine += line[i];
            if (i < numGaps) {
                justifiedLine += ' '.repeat(spacesPerGap + (i < extraSpaces ? 1 : 0));
            }
        }

        return justifiedLine;
    }
}


  ```
  