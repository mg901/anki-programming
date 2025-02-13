## [Readonly 2](https://github.com/type-challenges/type-challenges/blob/main/questions/00008-medium-readonly-2/README.md)

<!-- notecardId: 1739479070510 -->

```ts
type MyReadonly2<T, U extends keyof T = keyof T> = Readonly<Pick<T, U>> &
  Omit<T, U>;
```
