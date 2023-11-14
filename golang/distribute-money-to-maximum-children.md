
  # distribute-money-to-maximum-children

  ```golang
  func distMoney(money int, children int) int {
    if money < children {
        return -1
    }

    money -= children

    eightChildren := money / 7
    restMoney := money % 7

    if eightChildren > children {
        return children - 1
    }

    if restMoney == 0 {
        return eightChildren
    }

    if restMoney != 3 {
        if eightChildren == children {
            return children - 1
        }
        return eightChildren
    }

    if eightChildren < children - 1 {
        return eightChildren
    }

    return eightChildren-1

}
  ```
  