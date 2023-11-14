
  # cache-with-time-limit

  ```javascript
  class TimeLimitedCache {
  constructor() {
    this.map = new Map();
  }

  set(key, value, duration) {
    const expirationTime = Date.now() + duration;
    const entry = { value, expirationTime };

    if (this.map.has(key)) {
      const existingEntry = this.map.get(key);
      if (existingEntry.expirationTime > Date.now()) {
        existingEntry.value = value;
        existingEntry.expirationTime = expirationTime;
        return true;
      }
    }

    this.map.set(key, entry);
    return false;
  }

  get(key) {
    const entry = this.map.get(key);
    if (entry && entry.expirationTime > Date.now()) {
      return entry.value;
    }
    return -1;
  }

  count() {
    let count = 0;
    for (const entry of this.map.values()) {
      if (entry.expirationTime > Date.now()) {
        count++;
      }
    }
    return count;
  }
}

  ```
  