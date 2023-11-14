
  # insert-delete-getrandom-o1

  ```javascript
  var RandomizedSet = function() {
    this.set = [];
    this.map = new Map();
};

RandomizedSet.prototype.insert = function(val) {
    if (this.map.has(val)) {
        return false;
    }
    
    this.set.push(val);
    this.map.set(val, this.set.length - 1);
    return true;
};

RandomizedSet.prototype.remove = function(val) {
    if (!this.map.has(val)) {
        return false;
    }
    
    const index = this.map.get(val);
    const lastElement = this.set[this.set.length - 1];
    
    // Swap the element to be removed with the last element in the set
    this.set[index] = lastElement;
    this.map.set(lastElement, index);
    
    // Remove the last element from the set and the map
    this.set.pop();
    this.map.delete(val);
    
    return true;
};

RandomizedSet.prototype.getRandom = function() {
    const randomIndex = Math.floor(Math.random() * this.set.length);
    return this.set[randomIndex];
};

/** 
 * Your RandomizedSet object will be instantiated and called as such:
 * var obj = new RandomizedSet()
 * var param_1 = obj.insert(val)
 * var param_2 = obj.remove(val)
 * var param_3 = obj.getRandom()
 */
  ```
  