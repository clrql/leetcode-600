
  # design-add-and-search-words-data-structure

  ```golang
  type TrieNode struct {
	children [26]*TrieNode
	isWord   bool
}

type WordDictionary struct {
	root *TrieNode
}

func Constructor() WordDictionary {
	return WordDictionary{
		root: &TrieNode{},
	}
}

func (this *WordDictionary) AddWord(word string) {
	node := this.root
	for _, ch := range word {
		index := ch - 'a'
		if node.children[index] == nil {
			node.children[index] = &TrieNode{}
		}
		node = node.children[index]
	}
	node.isWord = true
}

func (this *WordDictionary) Search(word string) bool {
	return this.searchHelper(word, 0, this.root)
}

func (this *WordDictionary) searchHelper(word string, index int, node *TrieNode) bool {
	if index == len(word) {
		return node.isWord
	}

	ch := word[index]
	if ch != '.' {
		child := node.children[ch-'a']
		if child != nil && this.searchHelper(word, index+1, child) {
			return true
		}
	} else {
		for _, child := range node.children {
			if child != nil && this.searchHelper(word, index+1, child) {
				return true
			}
		}
	}

	return false
}


/**
 * Your WordDictionary object will be instantiated and called as such:
 * obj := Constructor();
 * obj.AddWord(word);
 * param_2 := obj.Search(word);
 */
  ```
  