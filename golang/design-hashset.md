
  # design-hashset

  ```golang
  type MyHashSet struct {
	buckets []LinkedList
	size    int
}

type LinkedList struct {
	head *Node
}

type Node struct {
	key  int
	next *Node
}

func Constructor() MyHashSet {
	return MyHashSet{
		buckets: make([]LinkedList, 10000),
		size:    10000,
	}
}

func (this *MyHashSet) Add(key int) {
	hash := key % this.size
	bucket := &this.buckets[hash]

	// Check if the key already exists in the linked list
	current := bucket.head
	for current != nil {
		if current.key == key {
			return
		}
		current = current.next
	}

	// Add the key to the front of the linked list
	newNode := &Node{
		key:  key,
		next: bucket.head,
	}
	bucket.head = newNode
}

func (this *MyHashSet) Remove(key int) {
	hash := key % this.size
	bucket := &this.buckets[hash]

	// Check if the key exists in the linked list
	if bucket.head == nil {
		return
	}
	if bucket.head.key == key {
		bucket.head = bucket.head.next
		return
	}

	// Find the key and remove it from the linked list
	prev := bucket.head
	current := prev.next
	for current != nil {
		if current.key == key {
			prev.next = current.next
			return
		}
		prev = current
		current = current.next
	}
}

func (this *MyHashSet) Contains(key int) bool {
	hash := key % this.size
	bucket := &this.buckets[hash]

	// Check if the key exists in the linked list
	current := bucket.head
	for current != nil {
		if current.key == key {
			return true
		}
		current = current.next
	}

	return false
}

  ```
  