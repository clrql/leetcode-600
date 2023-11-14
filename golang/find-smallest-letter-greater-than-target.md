
  # find-smallest-letter-greater-than-target

  ```golang
  func nextGreatestLetter(letters []byte, target byte) byte {
    n := len(letters)
    start := 0
    end := n - 1

    for start <= end {
        mid := start + (end-start)/2
        if letters[mid] <= target {
            start = mid + 1
        } else {
            end = mid - 1
        }
    }

    if start < n {
        return letters[start]
    }
    return letters[0]
}

  ```
  