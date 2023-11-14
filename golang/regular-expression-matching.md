
  # regular-expression-matching

  ```golang
  func isMatch(s string, p string) bool {
    n, m := len(s), len(p)
    
    // Crear una matriz dp de (n+1) x (m+1) para almacenar los resultados de subproblemas
    dp := make([][]bool, n+1)
    for i := range dp {
        dp[i] = make([]bool, m+1)
    }

    // El patrón vacío solo puede emparejar una cadena vacía
    dp[0][0] = true
    
    // Si el patrón tiene un '*', el caracter anterior debe ser ignorado
    for j := 2; j <= m; j++ {
        if p[j-1] == '*' {
            dp[0][j] = dp[0][j-2]
        }
    }
    
    // Llenar la matriz dp utilizando la relación de recurrencia
    for i := 1; i <= n; i++ {
        for j := 1; j <= m; j++ {
            // Si los caracteres coinciden o el patrón tiene un punto, 
            // los resultados anteriores son relevantes
            if s[i-1] == p[j-1] || p[j-1] == '.' {
                dp[i][j] = dp[i-1][j-1]
            } else if p[j-1] == '*' {
                // Si el patrón tiene un '*', hay dos posibilidades:
                if s[i-1] == p[j-2] || p[j-2] == '.' {
                    // 1. Ignorar el '*' y el caracter anterior
                    // y comprobar si los subproblemas anteriores se resolvieron con éxito
                    dp[i][j] = dp[i][j-2] || 
                        // 2. O emparejar el caracter actual 
                        // y comprobar si el subproblema anterior se resolvió con éxito
                        dp[i-1][j]
                } else {
                    // El caracter anterior y el '*' no coinciden con el caracter actual, 
                    // por lo que solo podemos ignorarlos
                    dp[i][j] = dp[i][j-2]
                }
            }
        }
    }
    
    // El resultado final se encuentra en dp[n][m]
    return dp[n][m]
}


  ```
  