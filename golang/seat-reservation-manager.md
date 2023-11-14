
  # seat-reservation-manager

  ```golang
  type SeatManager struct {
    availableSeats *PriorityQueue
}

func Constructor(n int) SeatManager {
    pq := &PriorityQueue{}
    heap.Init(pq)

    for i := 1; i <= n; i++ {
        heap.Push(pq, i)
    }

    return SeatManager{pq}
}

func (this *SeatManager) Reserve() int {
    if this.availableSeats.Len() > 0 {
        return heap.Pop(this.availableSeats).(int)
    }
    return -1 // Or handle the case when all seats are reserved
}

func (this *SeatManager) Unreserve(seatNumber int) {
    heap.Push(this.availableSeats, seatNumber)
}

// PriorityQueue for managing available seats
type PriorityQueue []int

func (pq PriorityQueue) Len() int { return len(pq) }

func (pq PriorityQueue) Less(i, j int) bool { return pq[i] < pq[j] }

func (pq PriorityQueue) Swap(i, j int) { pq[i], pq[j] = pq[j], pq[i] }

func (pq *PriorityQueue) Push(x interface{}) {
    item := x.(int)
    *pq = append(*pq, item)
}

func (pq *PriorityQueue) Pop() interface{} {
    old := *pq
    n := len(old)
    item := old[n-1]
    *pq = old[0 : n-1]
    return item
}

/**
 * Your SeatManager object will be instantiated and called as such:
 * obj := Constructor(n);
 * param_1 := obj.Reserve();
 * obj.Unreserve(seatNumber);
 */
  ```
  