## [Chainable Options](https://github.com/type-challenges/type-challenges/blob/main/questions/00012-medium-chainable-options/README.md)

<!-- notecardId: 1739479080807 -->

```ts
type Chainable<T = {}> = {
  option: <K extends string, V>(
    key: K extends keyof T ? never : K,
    value: V
  ) => Chainable<Omit<T, K> & Record<K, V>>;
  get: () => T;
};
```
