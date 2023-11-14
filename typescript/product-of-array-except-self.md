
  # product-of-array-except-self

  ```typescript
  function productExceptSelf(nums: number[]): number[] {
    const n = nums.length;
    const output: number[] = new Array(n);
    
    // Calculate the product of all elements to the left of each element
    let leftProduct = 1;
    for (let i = 0; i < n; i++) {
        output[i] = leftProduct;
        leftProduct *= nums[i];
    }
    
    // Calculate the product of all elements to the right of each element
    let rightProduct = 1;
    for (let i = n - 1; i >= 0; i--) {
        output[i] *= rightProduct;
        rightProduct *= nums[i];
    }
    
    return output;
};
  ```
  