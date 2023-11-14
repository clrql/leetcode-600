
  # implement-queue-using-stacks

  ```golang
  type MyQueue struct {
	stack1 *list.List
	stack2 *list.List
}

func Constructor() MyQueue {
	return MyQueue{
		stack1: list.New(),
		stack2: list.New(),
	}
}

func (q *MyQueue) Push(x int) {
	q.stack1.PushBack(x)
}

func (q *MyQueue) Pop() int {
	if q.stack2.Len() == 0 {
		q.moveStack1ToStack2()
	}

	return q.stack2.Remove(q.stack2.Back()).(int)
}

func (q *MyQueue) Peek() int {
	if q.stack2.Len() == 0 {
		q.moveStack1ToStack2()
	}

	return q.stack2.Back().Value.(int)
}

func (q *MyQueue) Empty() bool {
	return q.stack1.Len() == 0 && q.stack2.Len() == 0
}

func (q *MyQueue) moveStack1ToStack2() {
	for q.stack1.Len() > 0 {
		value := q.stack1.Remove(q.stack1.Back()).(int)
		q.stack2.PushBack(value)
	}
}

/**
 * Your MyQueue object will be instantiated and called as such:
 * obj := Constructor();
 * obj.Push(x);
 * param_2 := obj.Pop();
 * param_3 := obj.Peek();
 * param_4 := obj.Empty();
 */

/*
In this implementation, we define a MyQueue struct that contains two stacks (stack1 and stack2) implemented using the container/list package.

The Constructor function initializes the MyQueue struct with the two stacks.

The Push method adds an element to the queue by pushing it onto stack1.

The Pop method removes and returns the element at the front of the queue. If stack2 is empty, it transfers all elements from stack1 to stack2 by calling the moveStack1ToStack2 method. Then, it removes and returns the element from the back of stack2.

The Peek method returns the element at the front of the queue without removing it. If stack2 is empty, it transfers all elements from stack1 to stack2 by calling the moveStack1ToStack2 method. Then, it returns the element at the back of stack2.

The Empty method checks if the queue is empty by examining the lengths of both stack1 and stack2.

The moveStack1ToStack2 method transfers all elements from stack1 to stack2 by removing elements from the back of stack1 and pushing them onto stack2.
*/
  ```
  