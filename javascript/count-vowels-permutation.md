
  # count-vowels-permutation

  ```javascript
  /**
 * @param {number} n
 * @return {number}
 */
var countVowelPermutation = function(n) {
    const MOD = 1000000007;
    
    // Inicializamos dp para n = 1
    let dp = [1, 1, 1, 1, 1];
    
    for (let i = 2; i <= n; i++) {
        // Creamos un nuevo arreglo para almacenar los valores actualizados
        let newDp = [0, 0, 0, 0, 0];
        
        // Reglas para cada vocal
        newDp[0] = (dp[1] + dp[2] + dp[4]) % MOD; // 'a' puede ser seguido por 'e', 'i' o 'u'
        newDp[1] = (dp[0] + dp[2]) % MOD; // 'e' puede ser seguido por 'a' o 'i'
        newDp[2] = (dp[1] + dp[3]) % MOD; // 'i' puede ser seguido por 'e' o 'o'
        newDp[3] = (dp[2]) % MOD; // 'o' puede ser seguido solo por 'i'
        newDp[4] = (dp[2] + dp[3]) % MOD; // 'u' puede ser seguido por 'i' o 'o'
        
        // Actualizamos dp con los nuevos valores
        dp = newDp;
    }
    
    // Sumamos todos los valores de dp y tomamos el módulo
    return dp.reduce((sum, val) => (sum + val) % MOD, 0);
};

  ```
  