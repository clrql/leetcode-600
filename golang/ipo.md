
  # ipo

  ```golang
  type project struct {
	capital int
	profit  int
}

type maxHeap []project

func (h maxHeap) Len() int           { return len(h) }
func (h maxHeap) Less(i, j int) bool { return h[i].profit > h[j].profit }
func (h maxHeap) Swap(i, j int)      { h[i], h[j] = h[j], h[i] }

func (h *maxHeap) Push(x interface{}) {
	*h = append(*h, x.(project))
}

func (h *maxHeap) Pop() interface{} {
	old := *h
	n := len(old)
	x := old[n-1]
	*h = old[:n-1]
	return x
}

func findMaximizedCapital(k int, w int, profits []int, capital []int) int {
	n := len(profits)
	projects := make([]project, n)
	for i := 0; i < n; i++ {
		projects[i] = project{capital[i], profits[i]}
	}

	sort.Slice(projects, func(i, j int) bool {
		return projects[i].capital < projects[j].capital
	})

	maxHeap := &maxHeap{}
	heap.Init(maxHeap)

	i := 0
	for k > 0 {
		for i < n && projects[i].capital <= w {
			heap.Push(maxHeap, projects[i])
			i++
		}

		if maxHeap.Len() == 0 {
			break
		}

		top := heap.Pop(maxHeap).(project)
		w += top.profit
		k--
	}

	return w
}
  ```
  