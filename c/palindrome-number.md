
  # palindrome-number

  ```c
  bool isPalindrome(int x) {
    // Negative numbers are not palindromes
    if (x < 0) {
        return false;
    }

    int original = x;
    long long reversed = 0; // Use long long to prevent overflow

    // Reverse the number
    while (x > 0) {
        int digit = x % 10;
        reversed = reversed * 10 + digit;
        x /= 10;
    }

    // Check if the reversed number is the same as the original
    return original == reversed;
}
  ```
  