
  # friends-of-appropriate-ages

  ```golang
  func numFriendRequests(ages []int) int {
    count := make([]int, 121)
    for _, age := range ages {
        count[age]++
    }
    
    ans := 0
    for ageA := 1; ageA <= 120; ageA++ {
        countA := count[ageA]
        for ageB := 1; ageB <= 120; ageB++ {
            countB := count[ageB]
            if float64(ageB) <= 0.5*float64(ageA)+float64(7) || ageB > ageA || (ageB > 100 && ageA < 100) {
                continue
            }
            ans += countA * countB
            if ageA == ageB {
                ans -= countA
            }
        }
    }
    return ans
}
  ```
  