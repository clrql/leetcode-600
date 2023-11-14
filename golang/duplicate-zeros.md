
  # duplicate-zeros

  ```golang
  func duplicateZeros(arr []int) {
    length := len(arr)
    
    for i := 0; i < length-1; i++ {
        if arr[i] == 0 {
            // Shift elements to the right starting from the end of the array
            for j := length - 1; j > i+1; j-- {
                arr[j] = arr[j-1]
            }
            // Duplicate the zero
            arr[i+1] = 0
            i++ // Skip the next element since we've already processed it
        }
    }
}

  ```
  