
  # valid-perfect-square

  ```golang
  func isPerfectSquare(num int) bool {
	if num < 1 {
		return false
	}

	left, right := 1, num

	for left <= right {
		mid := left + (right-left)/2
		square := mid * mid

		if square == num {
			return true
		} else if square < num {
			left = mid + 1
		} else {
			right = mid - 1
		}
	}

	return false
}

/*
In this implementation, the isPerfectSquare function takes a positive integer num and determines if it is a perfect square. It returns false if num is less than 1 since perfect squares are always positive integers.

We initialize left as 1 and right as num for the binary search. We continue the search until left is less than or equal to right. In each iteration, we calculate the square of the middle element (mid) using mid * mid. We then compare the calculated square with num. If they are equal, num is a perfect square, and we return true. If the calculated square is less than num, we update left to mid + 1 to search the upper half of the remaining range. Otherwise, if the calculated square is greater than num, we update right to mid - 1 to search the lower half of the remaining range.

If the search completes without finding a perfect square, the function returns false.
*/
  ```
  