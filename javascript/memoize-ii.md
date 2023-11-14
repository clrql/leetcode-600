
  # memoize-ii

  ```javascript
  /**
 * @param {Function} fn
 */
function memoize(fn) {
    const trie = new Trie();
  return function(...args) {
    let node = trie.root;
    for (let arg of args) {
      if (!node.has(arg)) {
        node.set(arg, new Map());
      }
      node = node.get(arg);
    }
    if (node.has("value")) {
      return node.get("value");
    }
    const result = fn(...args);
    node.set("value", result);
    return result;
  }
}

class Trie {
  constructor() {
    this.root = new Map();
  }

  // Inserts a new value into the trie.
  insert(keys, value) {
    let node = this.root;
    for (let key of keys) {
      if (!node.has(key)) {
        node.set(key, new Map());
      }
      node = node.get(key);
    }
    node.set("value", value);
  }

  // Gets the memoized value for a given set of keys, or undefined if not found.
  lookup(keys) {
    let node = this.root;
    for (let key of keys) {
      if (!node.has(key)) {
        return undefined;
      }
      node = node.get(key);
    }
    return node.get("value");
  }
}


/** 
 * let callCount = 0;
 * const memoizedFn = memoize(function (a, b) {
 *	 callCount += 1;
 *   return a + b;
 * })
 * memoizedFn(2, 3) // 5
 * memoizedFn(2, 3) // 5
 * console.log(callCount) // 1 
 */
  ```
  