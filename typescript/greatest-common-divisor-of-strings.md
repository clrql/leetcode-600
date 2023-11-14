
  # greatest-common-divisor-of-strings

  ```typescript
  function gcdOfStrings(str1: string, str2: string): string {
    if (str1 + str2 !== str2 + str1) {
        // The strings cannot be divided into each other evenly
        return "";
    }

    // Find the greatest common divisor of the lengths
    const gcdLength = gcd(str1.length, str2.length);

    // Extract the substring with length gcdLength from str1
    return str1.substr(0, gcdLength);
    }

    // Helper function to calculate the greatest common divisor using Euclidean algorithm
    function gcd(a: number, b: number): number {
    while (b !== 0) {
        const temp = b;
        b = a % b;
        a = temp;
    }
    return a;
};
  ```
  