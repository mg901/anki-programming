## [EventEmitter 2](https://www.greatfrontend.com/questions/javascript/event-emitter-ii?language=js)

<!-- notecardId: 1739475840094 -->

```js
class EventEmitter {
  #subscriptions = new Map();

  on(eventName, listener) {
    const subscriptions = this.#subscriptions;
    const hasName = subscriptions.has(eventName);

    if (!hasName) {
      subscriptions.set(eventName, []);
    }

    const listeners = subscriptions.get(eventName);
    listeners.push(listener);

    return {
      off() {
        if (hasName) {
          const index = listeners.findIndex((item) => item === listener);

          if (index > -1) {
            listeners.splice(index, 1);
          }

          if (!listeners.length) {
            subscriptions.delete(eventName);
          }
        }
      },
    };
  }

  emit(eventName, ...args) {
    if (!this.#subscriptions.has(eventName)) return false;

    const listeners = this.#subscriptions.get(eventName);

    listeners.forEach((listener) => {
      listener(...args);
    });

    return true;
  }
}
```
