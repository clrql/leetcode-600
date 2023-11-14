
  # convert-a-number-to-hexadecimal

  ```golang
  func toHex(num int) string {
	if num == 0 {
		return "0"
	}

	// Define the hexadecimal digits
	digits := "0123456789abcdef"
	result := ""

	// Convert negative numbers to their two's complement form
	if num < 0 {
		num += 1 << 32
	}

	// Convert the number to hexadecimal
	for num > 0 {
		// Extract the last four bits of the number
		digit := num & 0xf

		// Prepend the corresponding hexadecimal digit
		result = string(digits[digit]) + result

		// Right shift the number by four bits
		num >>= 4
	}

	return result
}

/*
In this implementation, the toHex function takes an integer num and converts it into its hexadecimal representation as a string.

We start by checking if num is equal to 0. If it is, we simply return "0" as the hexadecimal representation.

Next, we define a string digits that contains the hexadecimal digits from 0 to f. This string will be used to map the extracted digits to their corresponding hexadecimal characters.

If num is negative, we convert it to its two's complement form by adding 1 << 32 (the length of an integer in bits) to it.

To convert the number to hexadecimal, we repeatedly extract the last four bits of the number using bitwise AND with 0xf. We prepend the corresponding hexadecimal digit to the result string using string indexing.

After extracting the digit, we right shift the number by four bits to move to the next four bits.

Finally, we return the result string as the hexadecimal representation of the given number.
*/
  ```
  