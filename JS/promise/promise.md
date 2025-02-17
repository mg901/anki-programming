## [Promise](https://bigfrontend.dev/problem/create-your-own-Promise)

<!-- notecardId: 1739799132141 -->

```js
const STATES = {
  PENDING: "pending",
  FULFILLED: "fulfilled",
  REJECTED: "rejected",
};

const REACTION_TYPES = {
  FULFILL: "fulfill",
  REJECT: "reject",
};

class MyPromise {
  #result;

  #state = STATES.PENDING;

  #fulfilledReactions = [];

  #rejectedReactions = [];

  // https://tc39.es/ecma262/#sec-promise.resolve
  static resolve(value) {
    if (value instanceof MyPromise) {
      return value;
    }

    return new MyPromise((resolve) => resolve(value));
  }

  // https://tc39.es/ecma262/#sec-promise.reject
  static reject(reason) {
    return new MyPromise((_, reject) => reject(reason));
  }

  // https://tc39.es/ecma262/#sec-promise-executor
  constructor(executor) {
    const { resolve, reject } = this.#createResolvingFunctions();

    try {
      executor(resolve, reject);
    } catch (error) {
      reject(error);
    }
  }

  // https://tc39.es/ecma262/#sec-createresolvingfunctions
  #createResolvingFunctions() {
    let alreadyResolved = false;

    // https://tc39.es/ecma262/#sec-promise-resolve-functions
    const resolve = (resolution) => {
      if (alreadyResolved) return;
      alreadyResolved = true;

      try {
        if (this === resolution) {
          const { name } = resolution.constructor;

          throw new TypeError(`Chaining cycle detected for promise #<${name}>`);
        }

        if (!isObject(resolution)) {
          this.#fulfillPromise(resolution);

          return;
        }

        if (!isCallable(resolution.then)) {
          this.#fulfillPromise(resolution);

          return;
        }

        queueMicrotask(() => {
          this.#resolveThenableJob(resolution);
        });
      } catch (error) {
        this.#rejectPromise(error);
      }
    };

    // https://tc39.es/ecma262/#sec-promise-reject-functions
    const reject = (reason) => {
      if (alreadyResolved) return;
      alreadyResolved = true;

      this.#rejectPromise(reason);
    };

    return {
      resolve,
      reject,
    };
  }

  // https://tc39.es/ecma262/#sec-fulfillpromise
  #fulfillPromise(value) {
    const reactions = this.#fulfilledReactions;

    this.#result = value;
    this.#fulfilledReactions = undefined;
    this.#rejectedReactions = undefined;
    this.#state = STATES.FULFILLED;

    triggerReactions(reactions, value);
  }

  // https://tc39.es/ecma262/#sec-rejectpromise
  #rejectPromise(reason) {
    const reactions = this.#rejectedReactions;

    this.#result = reason;
    this.#fulfilledReactions = undefined;
    this.#rejectedReactions = undefined;
    this.#state = STATES.REJECTED;

    triggerReactions(reactions, reason);
  }

  // https://tc39.es/ecma262/#sec-newpromiseresolvethenablejob
  #resolveThenableJob(resolution) {
    const { resolve, reject } = this.#createResolvingFunctions();

    try {
      resolution.then(resolve, reject);
    } catch (error) {
      reject(error);
    }
  }

  // https://tc39.es/ecma262/#sec-promise.prototype.then
  then(onfulfilled, onrejected) {
    const onFulfilledJobCallback = isCallable(onfulfilled) ? onfulfilled : null;
    const onRejectedJobCallback = isCallable(onrejected) ? onrejected : null;

    const resultCapability = newPromiseCapability(MyPromise);

    const fulfilledReaction = {
      capability: resultCapability,
      type: REACTION_TYPES.FULFILL,
      handler: onFulfilledJobCallback,
    };

    const rejectedReaction = {
      capability: resultCapability,
      type: REACTION_TYPES.REJECT,
      handler: onRejectedJobCallback,
    };

    if (this.#state === STATES.PENDING) {
      this.#fulfilledReactions.push(fulfilledReaction);
      this.#rejectedReactions.push(rejectedReaction);
    } else if (this.#state === STATES.FULFILLED) {
      queueMicrotask(() => {
        reactionJob(fulfilledReaction, this.#result);
      });
    } else {
      queueMicrotask(() => {
        reactionJob(rejectedReaction, this.#result);
      });
    }

    return resultCapability.promise;
  }

  // https://tc39.es/ecma262/#sec-promise.prototype.catch
  catch(onrejected) {
    return this.then(null, onrejected);
  }
}

// https://tc39.es/ecma262/#sec-object-type
function isObject(it) {
  return typeof it === "object" ? it !== null : typeof it === "function";
}

// https://tc39.es/ecma262/#sec-newpromisecapability
function newPromiseCapability(C) {
  let resolve, reject;

  const promise = new C((res, rej) => {
    resolve = res;
    reject = rej;
  });

  return {
    promise,
    resolve,
    reject,
  };
}

function isCallable(it) {
  return typeof it === "function";
}

// https://tc39.es/ecma262/#sec-triggerpromisereactions
function triggerReactions(reactions, argument) {
  for (const reaction of reactions) {
    queueMicrotask(() => {
      reactionJob(reaction, argument);
    });
  }
}

// https://tc39.es/ecma262/#sec-newpromisereactionjob
function reactionJob(reaction, argument) {
  const { type, handler } = reaction;
  const { resolve, reject } = reaction.capability;

  try {
    if (!handler) {
      if (type === REACTION_TYPES.FULFILL) {
        resolve(argument);
      } else {
        reject(argument);
      }

      return;
    }

    const result = handler(argument);
    resolve(result);
  } catch (error) {
    reject(error);
  }
}
```
