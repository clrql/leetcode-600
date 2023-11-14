
  # baseball-game

  ```golang
  func calPoints(operations []string) int {
    stack := make([]int, 0)

    for _, op := range operations {
        switch op {
        case "C":
            stack = stack[:len(stack)-1]
        case "D":
            score := stack[len(stack)-1] * 2
            stack = append(stack, score)
        case "+":
            score := stack[len(stack)-1] + stack[len(stack)-2]
            stack = append(stack, score)
        default:
            score, _ := strconv.Atoi(op)
            stack = append(stack, score)
        }
    }

    sum := 0
    for _, score := range stack {
        sum += score
    }

    return sum
}

  ```
  