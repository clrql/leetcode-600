
  # count-number-of-homogenous-substrings

  ```golang
  func countHomogenous(s string) int {
    const mod int = 1000000007
    result := 0
    count := 1

    for i := 1; i < len(s); i++ {
        if s[i] == s[i-1] {
            count++
        } else {
            result = (result + count*(count+1)/2) % mod
            count = 1
        }
    }

    // Add the count for the last homogenous substring
    result = (result + count*(count+1)/2) % mod

    return result
}

  ```
  