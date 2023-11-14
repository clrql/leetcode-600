
  # implement-trie-prefix-tree

  ```golang
  type TrieNode struct {
	children map[rune]*TrieNode
	isWord   bool
}

type Trie struct {
	root *TrieNode
}

func Constructor() Trie {
	return Trie{
		root: &TrieNode{
			children: make(map[rune]*TrieNode),
			isWord:   false,
		},
	}
}

func (this *Trie) Insert(word string) {
	node := this.root
	for _, ch := range word {
		if _, ok := node.children[ch]; !ok {
			node.children[ch] = &TrieNode{
				children: make(map[rune]*TrieNode),
				isWord:   false,
			}
		}
		node = node.children[ch]
	}
	node.isWord = true
}

func (this *Trie) Search(word string) bool {
	node := this.searchPrefix(word)
	return node != nil && node.isWord
}

func (this *Trie) StartsWith(prefix string) bool {
	node := this.searchPrefix(prefix)
	return node != nil
}

func (this *Trie) searchPrefix(prefix string) *TrieNode {
	node := this.root
	for _, ch := range prefix {
		if _, ok := node.children[ch]; !ok {
			return nil
		}
		node = node.children[ch]
	}
	return node
}


/**
 * Your Trie object will be instantiated and called as such:
 * obj := Constructor();
 * obj.Insert(word);
 * param_2 := obj.Search(word);
 * param_3 := obj.StartsWith(prefix);
 */
  ```
  