
  # lru-cache

  ```golang
  type LRUCache struct {
    capacity int
    cache    map[int]*list.Element
    list     *list.List
}

type entry struct {
    key   int
    value int
}

func Constructor(capacity int) LRUCache {
    return LRUCache{
        capacity: capacity,
        cache:    make(map[int]*list.Element),
        list:     list.New(),
    }
}

func (this *LRUCache) Get(key int) int {
    if elem, ok := this.cache[key]; ok {
        this.list.MoveToFront(elem)
        return elem.Value.(*entry).value
    }
    return -1
}

func (this *LRUCache) Put(key int, value int) {
    if elem, ok := this.cache[key]; ok {
        elem.Value.(*entry).value = value
        this.list.MoveToFront(elem)
    } else {
        if this.list.Len() == this.capacity {
            lastElem := this.list.Back()
            delete(this.cache, lastElem.Value.(*entry).key)
            this.list.Remove(lastElem)
        }
        newElem := this.list.PushFront(&entry{key: key, value: value})
        this.cache[key] = newElem
    }
}


/**
 * Your LRUCache object will be instantiated and called as such:
 * obj := Constructor(capacity);
 * param_1 := obj.Get(key);
 * obj.Put(key,value);
 */
  ```
  