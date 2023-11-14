
  # asteroid-collision

  ```golang
  func asteroidCollision(asteroids []int) []int {
	stack := make([]int, 0)

	for _, asteroid := range asteroids {
		collided := false

		for len(stack) > 0 && asteroid < 0 && stack[len(stack)-1] > 0 {
			if stack[len(stack)-1] < -asteroid {
				stack = stack[:len(stack)-1]
				continue
			} else if stack[len(stack)-1] == -asteroid {
				stack = stack[:len(stack)-1]
			}
			collided = true
			break
		}

		if !collided {
			stack = append(stack, asteroid)
		}
	}

	return stack
}

  ```
  