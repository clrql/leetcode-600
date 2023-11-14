
  # kth-largest-element-in-a-stream

  ```golang
  type KthLargest struct {
	heap *MinHeap
	k    int
}

func Constructor(k int, nums []int) KthLargest {
	h := &MinHeap{}
	heap.Init(h)

	for _, num := range nums {
		if h.Len() < k {
			heap.Push(h, num)
		} else if num > h.Peek() {
			heap.Pop(h)
			heap.Push(h, num)
		}
	}

	return KthLargest{
		heap: h,
		k:    k,
	}
}

func (kl *KthLargest) Add(val int) int {
	if kl.heap.Len() < kl.k {
		heap.Push(kl.heap, val)
	} else if val > kl.heap.Peek() {
		heap.Pop(kl.heap)
		heap.Push(kl.heap, val)
	}

	return kl.heap.Peek()
}

type MinHeap []int

func (h MinHeap) Len() int            { return len(h) }
func (h MinHeap) Less(i, j int) bool  { return h[i] < h[j] }
func (h MinHeap) Swap(i, j int)       { h[i], h[j] = h[j], h[i] }
func (h *MinHeap) Push(x interface{}) { *h = append(*h, x.(int)) }

func (h *MinHeap) Pop() interface{} {
	old := *h
	n := len(old)
	x := old[n-1]
	*h = old[:n-1]
	return x
}

func (h MinHeap) Peek() int {
	return h[0]
}

  ```
  