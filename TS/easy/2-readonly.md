## [Readonly](https://github.com/type-challenges/type-challenges/blob/main/questions/00007-easy-readonly/README.md)

<!-- notecardId: 1739477909539 -->

```ts
type Readonly<T> = {
  readonly [P in keyof T]: T[P];
};
```
