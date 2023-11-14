
  # merge-k-sorted-lists

  ```golang
  /**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
// ListNodeHeap implements the heap.Interface for ListNode slice
type ListNodeHeap []*ListNode

func (h ListNodeHeap) Len() int            { return len(h) }
func (h ListNodeHeap) Less(i, j int) bool  { return h[i].Val < h[j].Val }
func (h ListNodeHeap) Swap(i, j int)       { h[i], h[j] = h[j], h[i] }
func (h *ListNodeHeap) Push(x interface{}) { *h = append(*h, x.(*ListNode)) }
func (h *ListNodeHeap) Pop() interface{} {
	old := *h
	n := len(old)
	item := old[n-1]
	*h = old[0 : n-1]
	return item
}

func mergeKLists(lists []*ListNode) *ListNode {
	// Create a min-heap and initialize it with the heads of each linked list
	h := &ListNodeHeap{}
	heap.Init(h)

	for _, node := range lists {
		if node != nil {
			heap.Push(h, node)
		}
	}

	// Create a dummy node to build the merged list
	dummy := &ListNode{}
	curr := dummy

	// Continue merging until all lists are exhausted
	for h.Len() > 0 {
		minNode := heap.Pop(h).(*ListNode)
		curr.Next = minNode
		curr = curr.Next

		if minNode.Next != nil {
			heap.Push(h, minNode.Next)
		}
	}

	return dummy.Next
}
  ```
  