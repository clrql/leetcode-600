
  # number-of-ways-to-reorder-array-to-get-same-bst

  ```golang
  const mod = int(1e9) + 7

func numOfWays(nums []int) int {
	memo := make(map[string]int)
	return (countWays(nums, memo) - 1 + mod) % mod
}

func countWays(nums []int, memo map[string]int) int {
	if len(nums) <= 2 {
		return 1
	}

	key := toString(nums)
	if val, ok := memo[key]; ok {
		return val
	}

	left := make([]int, 0)
	right := make([]int, 0)

	root := nums[0]
	for i := 1; i < len(nums); i++ {
		if nums[i] < root {
			left = append(left, nums[i])
		} else {
			right = append(right, nums[i])
		}
	}

	leftCount := countWays(left, memo)
	rightCount := countWays(right, memo)

	result := comb(len(nums)-1, len(left))
	result = (result * leftCount) % mod
	result = (result * rightCount) % mod

	memo[key] = result
	return result
}

func comb(n, k int) int {
	if k > n/2 {
		k = n - k
	}
	res := 1
	for i := 1; i <= k; i++ {
		res = (res * (n - i + 1)) % mod
		res = (res * modInverse(i)) % mod
	}
	return res
}

func modInverse(a int) int {
	res := 1
	exp := mod - 2
	for exp > 0 {
		if exp%2 == 1 {
			res = (res * a) % mod
		}
		a = (a * a) % mod
		exp >>= 1
	}
	return res
}

func toString(nums []int) string {
	str := ""
	for _, num := range nums {
		str += strconv.Itoa(num)
	}
	return str
}

  ```
  