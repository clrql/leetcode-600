
  # find-the-difference

  ```golang
  func findTheDifference(s string, t string) byte {
	var result byte

	for i := 0; i < len(s); i++ {
		result ^= s[i] ^ t[i]
	}
	result ^= t[len(t)-1]

	return result
}

/*
In this implementation, the findTheDifference function takes two strings s and t and returns the extra letter added to t.

We iterate over the characters of s using a for loop and perform XOR (^) operation between the characters of s and t at each position. This XOR operation cancels out the corresponding bits between the characters, leaving only the extra letter in the result. Finally, we perform XOR between the result and the last character of t to include the extra letter added at the end.
*/
  ```
  