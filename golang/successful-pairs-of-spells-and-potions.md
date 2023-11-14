
  # successful-pairs-of-spells-and-potions

  ```golang
  func successfulPairs(spells []int, potions []int, success int64) []int {
	sort.Ints(potions)
	answer := make([]int, 0)
	m := len(potions)
	maxPotion := potions[m-1]

	for _, spell := range spells {
		minPotion := int(math.Ceil(float64(success) / float64(spell)))
		if minPotion > maxPotion {
			answer = append(answer, 0)
			continue
		}
		index := lowerBound(potions, minPotion)
		answer = append(answer, m-index)
	}

	return answer
}

func lowerBound(arr []int, key int) int {
	low := 0
	high := len(arr)
	for low < high {
		mid := (low + high) / 2
		if arr[mid] < key {
			low = mid + 1
		} else {
			high = mid
		}
	}
	return low
}
  ```
  