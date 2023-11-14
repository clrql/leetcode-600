
  # prime-number-of-set-bits-in-binary-representation

  ```golang
  func countPrimeSetBits(left int, right int) int {
	count := 0

	for num := left; num <= right; num++ {
		bitCount := countSetBits(num)
		if isPrime(bitCount) {
			count++
		}
	}

	return count
}

func countSetBits(num int) int {
	count := 0

	for num > 0 {
		if num&1 == 1 {
			count++
		}
		num >>= 1
	}

	return count
}

func isPrime(num int) bool {
	if num <= 1 {
		return false
	}

	for i := 2; i*i <= num; i++ {
		if num%i == 0 {
			return false
		}
	}

	return true
}

  ```
  