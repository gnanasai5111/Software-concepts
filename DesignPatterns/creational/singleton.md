## Singleton
- Singletons are classes that allow only one instance to be created.
- This instance is shared globally and reused across the entire application.
- Useful for managing global state, such as configurations, counters, logging, caching, etc.


```
let instance;
let count = 0;

class Counter {
  constructor() {
    if (instance) {
      throw new Error("You can only create one instance!");
    }
    instance = this;
  }
  getInstance() {
    return this;
  }
  getCount() {
    return count;
  }
  increment() {
    return ++count;
  }
  decrement() {
    return --count;
  }
}
// Freezing to prevent modification of instance structure
const singletonCounter = Object.freeze(new Counter());


export default singletonCounter
```

- instance ensures that only one object of the class is created.
- Object.freeze() prevents modifying or adding properties, but methods can still update internal logic/state.
- count is module-level (private to the file), not tied to the class instance.
- Calling singletonCounter.increment() multiple times will update count globally.

## Usage
```
import counter from './Counter';

counter.increment(); // 1
counter.increment(); // 2
console.log(counter.getCount());
```
