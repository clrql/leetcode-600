
  # valid-mountain-array

  ```golang
  func validMountainArray(arr []int) bool {
    n := len(arr)
    if n < 3 {
        return false
    }
    
    // Find the peak of the mountain
    peak := 0
    for peak < n-1 && arr[peak] < arr[peak+1] {
        peak++
    }
    
    // Check if the peak is not at the beginning or end
    if peak == 0 || peak == n-1 {
        return false
    }
    
    // Check if the right side of the peak is decreasing
    for i := peak; i < n-1; i++ {
        if arr[i] <= arr[i+1] {
            return false
        }
    }
    
    return true   
}
  ```
  