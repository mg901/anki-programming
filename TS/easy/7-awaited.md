## [Awaited](https://github.com/type-challenges/type-challenges/blob/main/questions/00189-easy-awaited/README.md)

<!-- notecardId: 1739478101235 -->

```ts
type MyAwaited<T extends PromiseLike<any>> = T extends PromiseLike<infer R>
  ? R extends PromiseLike<any>
    ? MyAwaited<R>
    : R
  : never;

// or source implementation
type Awaited<T> = T extends null | undefined
  ? T
  : T extends object & { then(onfulfilled: infer R, ...args: infer _): any }
  ? R extends (value: infer Value, ...args: infer _) => any
    ? Awaited<Value>
    : never
  : T;
```
