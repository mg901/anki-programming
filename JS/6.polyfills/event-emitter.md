## [Event Emitter](https://www.greatfrontend.com/interviews/study/data-structures-algorithms/questions/javascript/event-emitter)

```js
export default class EventEmitter {
  constructor() {
    this.listenersByName = new Map();
  }

  on(eventName, listener) {
    let listeners = this.listenersByName.get(eventName);

    if (!listeners) {
      listeners = [];
      this.listenersByName.set(eventName, listeners);
    }

    listeners.push(listener);

    return this;
  }

  off(eventName, listener) {
    const listeners = this.listenersByName.get(eventName);
    if (!listeners) return this;

    const index = listeners.indexOf(listener);

    if (index > -1) {
      listeners.splice(index, 1);

      if (listeners.length === 0) {
        this.listenersByName.delete(eventName);
      }
    }

    return this;
  }

  emit(eventName, ...args) {
    const listeners = this.listenersByName.get(eventName);
    if (!listeners) return false;

    for (const listener of listeners) {
      listener(...args);
    }

    return true;
  }
}
```
