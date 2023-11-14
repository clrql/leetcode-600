
  # design-authentication-manager

  ```golang
  type AuthenticationManager struct {
    Hash map[string]int
    timeToLive int
}


func Constructor(timeToLive int) AuthenticationManager {
    var a AuthenticationManager
    a.timeToLive = timeToLive
    a.Hash = make(map[string]int)
    return a
}


func (this *AuthenticationManager) Generate(tokenId string, currentTime int)  {
    this.Hash[tokenId] = currentTime + this.timeToLive
} 


func (this *AuthenticationManager) Renew(tokenId string, currentTime int)  {
    if _, ok := this.Hash[tokenId]; ok && this.Hash[tokenId] > currentTime {
        this.Hash[tokenId] = currentTime + this.timeToLive
    }
}


func (this *AuthenticationManager) CountUnexpiredTokens(currentTime int) int {
    for key, val := range this.Hash {
        if (val <= currentTime) {
            delete(this.Hash, key)
        }
    }
    return len(this.Hash)
}


/**
 * Your AuthenticationManager object will be instantiated and called as such:
 * obj := Constructor(timeToLive);
 * obj.Generate(tokenId,currentTime);
 * obj.Renew(tokenId,currentTime);
 * param_3 := obj.CountUnexpiredTokens(currentTime);
 */
  ```
  