
  # poor-pigs

  ```golang
  func poorPigs(buckets int, minutesToDie int, minutesToTest int) int {
    // Calculate the number of tests we can perform
    tests := minutesToTest/minutesToDie + 1

    // Calculate the number of pigs needed
    pigs := 0
    for pow := 1; pow < buckets; pow *= tests {
        pigs++
    }

    return pigs
}
  ```
  