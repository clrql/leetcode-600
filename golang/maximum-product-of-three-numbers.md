
  # maximum-product-of-three-numbers

  ```golang
  func maximumProduct(nums []int) int {
    // Sort the array in ascending order
    sort.Ints(nums)

    // Calculate the two possible products
    product1 := nums[len(nums)-1] * nums[len(nums)-2] * nums[len(nums)-3]
    product2 := nums[0] * nums[1] * nums[len(nums)-1]

    // Return the maximum product
    if product1 > product2 {
        return product1
    } else {
        return product2
    }
}

  ```
  