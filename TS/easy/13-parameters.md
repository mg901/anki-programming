## [Parameters](https://github.com/type-challenges/type-challenges/blob/main/questions/03312-easy-parameters/README.md)

<!-- notecardId: 1739477950808 -->

```ts
type MyParameters<T extends (...args: any[]) => any> = T extends (
  ...args: infer Args
) => any
  ? Args
  : [];
```
