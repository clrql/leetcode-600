
  # top-k-frequent-elements

  ```golang
  type Item struct {
	value    int
	frequency int
}

type MinHeap []*Item

func (h MinHeap) Len() int           { return len(h) }
func (h MinHeap) Less(i, j int) bool { return h[i].frequency < h[j].frequency }
func (h MinHeap) Swap(i, j int)      { h[i], h[j] = h[j], h[i] }

func (h *MinHeap) Push(x interface{}) {
	*h = append(*h, x.(*Item))
}

func (h *MinHeap) Pop() interface{} {
	old := *h
	n := len(old)
	item := old[n-1]
	*h = old[0 : n-1]
	return item
}

func topKFrequent(nums []int, k int) []int {
	frequencyMap := make(map[int]int)

	// Build frequency map
	for _, num := range nums {
		frequencyMap[num]++
	}

	// Create a min-heap
	h := &MinHeap{}

	// Insert elements into the heap
	for value, frequency := range frequencyMap {
		item := &Item{
			value:    value,
			frequency: frequency,
		}
		heap.Push(h, item)
		if h.Len() > k {
			heap.Pop(h)
		}
	}

	// Extract the top k frequent elements from the heap
	result := make([]int, k)
	for i := k - 1; i >= 0; i-- {
		result[i] = heap.Pop(h).(*Item).value
	}

	return result
}
  ```
  