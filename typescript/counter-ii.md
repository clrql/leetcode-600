
  # counter-ii

  ```typescript
  type ReturnObj = {
  increment: () => number;
  decrement: () => number;
  reset: () => number;
};

function createCounter(init: number): ReturnObj {
  let current: number = init;

  return {
    increment: () => {
      current += 1;
      return current;
    },
    decrement: () => {
      current -= 1;
      return current;
    },
    reset: () => {
      current = init;
      return current;
    },
  };
}

/**
 * const counter = createCounter(5)
 * counter.increment(); // 6
 * counter.reset(); // 5
 * counter.decrement(); // 4
 */
  ```
  