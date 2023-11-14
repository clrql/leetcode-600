
  # implement-stack-using-queues

  ```golang
  type MyStack struct {
	queue1 *list.List
	queue2 *list.List
	topVal int
}

func Constructor() MyStack {
	return MyStack{
		queue1: list.New(),
		queue2: list.New(),
		topVal: 0,
	}
}

func (s *MyStack) Push(x int) {
	s.topVal = x
	s.queue1.PushBack(x)
}

func (s *MyStack) Pop() int {
	for s.queue1.Len() > 1 {
		s.topVal = s.queue1.Remove(s.queue1.Front()).(int)
		s.queue2.PushBack(s.topVal)
	}

	value := s.queue1.Remove(s.queue1.Front())
	s.queue1, s.queue2 = s.queue2, s.queue1

	return value.(int)
}

func (s *MyStack) Top() int {
	return s.topVal
}

func (s *MyStack) Empty() bool {
	return s.queue1.Len() == 0
}

/**
 * Your MyStack object will be instantiated and called as such:
 * obj := Constructor();
 * obj.Push(x);
 * param_2 := obj.Pop();
 * param_3 := obj.Top();
 * param_4 := obj.Empty();
 */

/*
In this implementation, we define a MyStack struct that contains two queues (queue1 and queue2) implemented using the container/list package. We also keep track of the top value of the stack (topVal). The Constructor function initializes the struct with the two queues and the top value set to 0.

The Push method adds an element to the stack by pushing it to queue1 and updating the top value accordingly.

The Pop method removes and returns the element at the top of the stack. It transfers all elements from queue1 to queue2, except for the last element which becomes the new top value. Then, it swaps the queues and returns the last element from the original queue1.

The Top method returns the top value of the stack without removing it.

The Empty method checks if the stack is empty by examining the length of queue1. 
*/
  ```
  