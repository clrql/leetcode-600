
  # minimum-genetic-mutation

  ```javascript
  /**
 * @param {string} startGene
 * @param {string} endGene
 * @param {string[]} bank
 * @return {number}
 */
var minMutation = function(startGene, endGene, bank) {
  // Check if the endGene is not in the bank
  if (!bank.includes(endGene)) {
    return -1;
  }
  
  // Create a set to keep track of visited genes
  const visited = new Set();
  
  // Create a queue for BFS
  const queue = [];
  
  // Enqueue the startGene with 0 mutations
  queue.push([startGene, 0]);
  
  while (queue.length > 0) {
    const [gene, mutations] = queue.shift();
    
    // Check if we have reached the endGene
    if (gene === endGene) {
      return mutations;
    }
    
    // Explore all possible mutations
    for (const nextGene of bank) {
      if (!visited.has(nextGene) && isMutation(gene, nextGene)) {
        visited.add(nextGene);
        queue.push([nextGene, mutations + 1]);
      }
    }
  }
  
  // If we reach here, it means there is no valid mutation
  return -1;
};

// Helper function to check if two genes are a valid mutation
function isMutation(gene1, gene2) {
  let diff = 0;
  
  for (let i = 0; i < gene1.length; i++) {
    if (gene1[i] !== gene2[i]) {
      diff++;
    }
  }
  
  return diff === 1;
}
  ```
  