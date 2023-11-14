
  # broken-calculator

  ```golang
  func brokenCalc(startValue int, target int) int {   
    operations := 0

    for target > startValue {
        if target % 2 == 0 {
            target /= 2
        } else {
            target += 1
        }
        operations++
    }

    return operations + startValue - target
}

/* 
    Allowed operations are "*2" and "-1".

    if startNumber -

*/
  ```
  