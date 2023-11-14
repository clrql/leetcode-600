
  # bitwise-and-of-numbers-range

  ```golang
  func rangeBitwiseAnd(left int, right int) int {
	shifts := 0

	// Find the common prefix of the binary representations
	// by counting the number of right shifts required to make
	// left and right equal.
	for left != right {
		left >>= 1
		right >>= 1
		shifts++
	}

	// Shift left back by the number of shifts performed
	// to obtain the bitwise AND result.
	return left << shifts
}
  ```
  