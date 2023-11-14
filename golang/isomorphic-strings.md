
  # isomorphic-strings

  ```golang
  func isIsomorphic(s string, t string) bool {
    if len(s) != len(t) {
        return false
    }
    
    sMap := make(map[byte]byte)
    tMap := make(map[byte]byte)
    
    for i := 0; i < len(s); i++ {
        sChar, sExists := sMap[s[i]]
        tChar, tExists := tMap[t[i]]
        
        if sExists != tExists || (sExists && sChar != t[i]) || (tExists && tChar != s[i]) {
            return false
        }
        
        sMap[s[i]] = t[i]
        tMap[t[i]] = s[i]
    }
    
    return true
}

  ```
  