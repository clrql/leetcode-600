
  # lemonade-change

  ```golang
  func lemonadeChange(bills []int) bool {
    // Variables to keep track of the available bills
    fiveBillCount := 0
    tenBillCount := 0
    
    for _, bill := range bills {
        switch bill {
        case 5:
            // Collect a $5 bill
            fiveBillCount++
        case 10:
            // Collect a $10 bill and give back a $5
            if fiveBillCount > 0 {
                fiveBillCount--
                tenBillCount++
            } else {
                return false
            }
        case 20:
            // Collect a $20 bill
            // Give back change of $15 (a $10 bill and a $5 bill)
            if tenBillCount > 0 && fiveBillCount > 0 {
                tenBillCount--
                fiveBillCount--
            } else if fiveBillCount >= 3 {
                fiveBillCount -= 3
            } else {
                return false
            }
        }
    }
    
    return true
}

  ```
  