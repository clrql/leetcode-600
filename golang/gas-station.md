
  # gas-station

  ```golang
  func canCompleteCircuit(gas []int, cost []int) int {
    totalGas := 0
    currentGas := 0
    startIndex := 0

    for i := 0; i < len(gas); i++ {
        totalGas += gas[i] - cost[i]
        currentGas += gas[i] - cost[i]

        if currentGas < 0 {
            // Start from the next station
            startIndex = i + 1
            currentGas = 0
        }
    }

    if totalGas < 0 {
        // Total gas is negative, can't complete the circuit
        return -1
    }

    return startIndex
}
  ```
  