
  # 3sum-closest

  ```golang
  func threeSumClosest(nums []int, target int) int {
    // Ordena la lista de números para simplificar el proceso de búsqueda.
    sort.Ints(nums)
    
    closest := nums[0] + nums[1] + nums[2]
    
    for i := 0; i < len(nums) - 2; i++ {
        left, right := i+1, len(nums)-1
        
        for left < right {
            sum := nums[i] + nums[left] + nums[right]
            
            if abs(sum - target) < abs(closest - target) {
                closest = sum
            }
            
            if sum < target {
                left++
            } else if sum > target {
                right--
            } else {
                // No puedes obtener una suma más cercana que esta, así que retorna inmediatamente.
                return sum
            }
        }
    }
    
    return closest
}

func abs(x int) int {
    if x < 0 {
        return -x
    }
    return x
}
  ```
  