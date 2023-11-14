
  # word-search-ii

  ```golang
  type TrieNode struct {
	children [26]*TrieNode
	word     string
}

func buildTrie(words []string) *TrieNode {
	root := &TrieNode{}

	for _, word := range words {
		node := root
		for _, ch := range word {
			index := ch - 'a'
			if node.children[index] == nil {
				node.children[index] = &TrieNode{}
			}
			node = node.children[index]
		}
		node.word = word
	}

	return root
}

func findWords(board [][]byte, words []string) []string {
	// Build the trie from the given words
	trie := buildTrie(words)

	// Perform backtracking for each cell in the board
	result := make([]string, 0)
	for i := 0; i < len(board); i++ {
		for j := 0; j < len(board[0]); j++ {
			backtrack(board, i, j, trie, &result)
		}
	}

	return result
}

func backtrack(board [][]byte, row, col int, trie *TrieNode, result *[]string) {
	ch := board[row][col]
	if ch == '#' || trie.children[ch-'a'] == nil {
		return
	}

	trie = trie.children[ch-'a']
	if trie.word != "" {
		*result = append(*result, trie.word)
		trie.word = ""
	}

	board[row][col] = '#'
	if row > 0 {
		backtrack(board, row-1, col, trie, result)
	}
	if col > 0 {
		backtrack(board, row, col-1, trie, result)
	}
	if row < len(board)-1 {
		backtrack(board, row+1, col, trie, result)
	}
	if col < len(board[0])-1 {
		backtrack(board, row, col+1, trie, result)
	}
	board[row][col] = ch
}

  ```
  