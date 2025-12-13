## [EventEmitter 2](https://www.greatfrontend.com/questions/javascript/event-emitter-ii?language=js)

<!-- notecardId: 1763487062479 -->

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

    return {
      off: () => {
        const index = listeners.indexOf(listener);

        if (index > -1) {
          listeners.splice(index, 1);

          if (listeners.length === 0) {
            this.listenersByName.delete(eventName);
          }
        }
      },
    };
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
