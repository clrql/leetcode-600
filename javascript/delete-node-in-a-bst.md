
  # delete-node-in-a-bst

  ```javascript
  /**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @param {number} key
 * @return {TreeNode}
 */
var deleteNode = function(root, key) {

    if (root === null) {
        return null;
    }

    if (key < root.val) {
        root.left = deleteNode(root.left, key);
    } else if (key > root.val) {
        root.right = deleteNode(root.right, key);
    } else {
        // Caso 1: Sin hijos o con un solo hijo
        if (root.left === null) {
            return root.right;
        } else if (root.right === null) {
            return root.left;
        }

        // Caso 2: Dos hijos
        // Encontrar el valor minimo en el subarbol a la derecha
        var minValue = findMinValue(root.right);
        root.val = minValue;

        // Eliminar el minimo nodo en el subarbol a la derecha
        root.right = deleteNode(root.right, minValue);
    }

    return root;
};

var findMinValue = function(root) {
    while (root.left !== null) {
        root = root.left
    }
    return root.val;
}
  ```
  