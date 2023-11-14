
  # eliminate-maximum-number-of-monsters

  ```golang
  func eliminateMaximum(dist []int, speed []int) int {
    n := len(dist)
    times := make([]float64, n)
    
    for i := 0; i < n; i++ {
        times[i] = float64(dist[i]) / float64(speed[i])
    }
    
    sort.Float64s(times)
    
    for i := 0; i < n; i++ {
        if float64(i) >= times[i] {
            return i
        }
    }
    
    return n
}

  ```
  