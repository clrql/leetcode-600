
  # count-primes

  ```rust
  impl Solution {
    pub fn count_primes(n: i32) -> i32 {
        let n = n as usize;
        if n <= 2 {return 0;}
        let mut validations: Vec<bool> = vec![true; n];
        validations.splice(0..2, [false;2]);
        for i in 2..=(n as f64).sqrt() as usize {
            if !validations[i] {continue}
            let mut j = i.pow(2);
            while j < n {
                validations[j] = false;
                j += i;
            }
        }
        validations.into_iter().filter(|&a| a).count() as i32
    }
}
  ```
  