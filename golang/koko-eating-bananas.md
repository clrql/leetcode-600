
  # koko-eating-bananas

  ```golang
  func minEatingSpeed(piles []int, h int) int {
    // Find the maximum pile size
    maxPile := 0
    for _, pile := range piles {
        if pile > maxPile {
            maxPile = pile
        }
    }
    
    // Binary search for the minimum eating speed
    left, right := 1, maxPile
    for left < right {
        mid := left + (right-left)/2
        if canEatAll(piles, h, mid) {
            right = mid
        } else {
            left = mid + 1
        }
    }
    
    return left
}

func canEatAll(piles []int, h, k int) bool {
    hours := 0
    for _, pile := range piles {
        hours += (pile + k - 1) / k
    }
    return hours <= h
}

  ```
  