
  # find-mode-in-binary-search-tree

  ```golang
  /**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func findMode(root *TreeNode) []int {
    var result []int // Un slice para almacenar los modos
    var prev *TreeNode // Un puntero al nodo previo para comparar con el nodo actual
    var currentCount, maxCount int // Contadores para el nodo actual y el nodo maximo
    
    // Funcion para realizar un recorrido in-order del arbol
    var inOrderTraversal func(node *TreeNode)
    inOrderTraversal = func(node *TreeNode) {
        if node == nil {
            return
        }

        // Recorrer el subarbol izquierdo
        inOrderTraversal(node.Left)

        // Comparar el valor del nodo actual con el nodo previo.
        if prev != nil && node.Val == prev.Val {
            currentCount ++
        } else {
            currentCount = 1
        }

        // Actualiza el nodo previo.
        prev = node

        // Comprueba si el conteo actual es mayor o igual al maximo conteo
        if currentCount == maxCount {
            // Agrega el valor actual al nodo
            result = append(result, node.Val)
        } else if currentCount > maxCount {
            // Nuevo valor con un conteo mayor
            result = []int{node.Val}
            maxCount = currentCount
        }

        // Recorre el subarbol derecho
        inOrderTraversal(node.Right)
    }

    // Inicializa la funcion de recorrido in-order desdde el nodo raiz
    inOrderTraversal(root)

    return result

}
  ```
  