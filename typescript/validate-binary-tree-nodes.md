
  # validate-binary-tree-nodes

  ```typescript
  function validateBinaryTreeNodes(n: number, leftChild: number[], rightChild: number[]): boolean {
    const childrenSet = new Set([...leftChild, ...rightChild]);
    let rootNode: number = null;
    for (let i = 0; i < n; i++) {
        if (! childrenSet.has(i)) {
            rootNode = i;
            break;
        }
    }

    // The binary tree have a root (root has no parent)
    if (rootNode === null) {
        return false;
    }

    const visited = new Set([rootNode]);
    const stack = [rootNode];

    while (stack.length > 0) {
        const node = stack.pop();
        for (const child of [leftChild[node], rightChild[node]]) {
            if (child == -1) continue;

            // Every node have 1 parent + There are no cycle
            if (visited.has(child)) {
                return false;
            }

            stack.push(child);
            visited.add(child);
        }
    }

    // Every node must be connected
    return visited.size == n;

};
  ```
  