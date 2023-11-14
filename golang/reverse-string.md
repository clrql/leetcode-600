
  # reverse-string

  ```golang
  func reverseString(s []byte) {
	left := 0
	right := len(s) - 1

	for left < right {
		s[left], s[right] = s[right], s[left]
		left++
		right--
	}
}

/*
In this implementation, the reverseString function takes an array of characters s and reverses it in-place. It initializes left and right pointers to the beginning and end of the array, respectively. It then iterates while left is less than right. In each iteration, it swaps the characters at the left and right positions using the tuple assignment s[left], s[right] = s[right], s[left], and increments left and decrements right. This process continues until the pointers meet or cross each other, resulting in the reversed array.
*/
  ```
  