
  # number-of-equivalent-domino-pairs

  ```golang
  func numEquivDominoPairs(dominoes [][]int) int {
    total := 0
    for i := 0; i < len(dominoes); i++ {
        for j := i+1; j < len(dominoes); j++ {
            if dominoes[i][0] == dominoes[j][0] && dominoes[i][1] == dominoes[j][1] || 
dominoes[i][0] == dominoes[j][1] && dominoes[i][1] == dominoes[j][0] {
                total += 1
            }
        }
    }
    return total
}
  ```
  