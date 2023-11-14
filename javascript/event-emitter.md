
  # event-emitter

  ```javascript
  class EventEmitter {
  constructor() {
    this.events = {};
    this.subscriptionId = 0;
  }

  subscribe(event, cb) {
    if (!this.events[event]) {
      this.events[event] = {};
    }

    const subscriptionId = this.subscriptionId++;
    this.events[event][subscriptionId] = cb;

    return {
      unsubscribe: () => {
        delete this.events[event][subscriptionId];
      },
    };
  }

  emit(event, args = []) {
    if (!this.events[event]) {
      return [];
    }

    const callbacks = Object.values(this.events[event]);
    return callbacks.map(cb => cb(...args));
  }
}


/**
 * const emitter = new EventEmitter();
 *
 * // Subscribe to the onClick event with onClickCallback
 * function onClickCallback() { return 99 }
 * const sub = emitter.subscribe('onClick', onClickCallback);
 *
 * emitter.emit('onClick'); // [99]
 * sub.unsubscribe(); // undefined
 * emitter.emit('onClick'); // []
 */
  ```
  