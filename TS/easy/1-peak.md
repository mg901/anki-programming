## [Pick](https://github.com/type-challenges/type-challenges/blob/main/questions/00004-easy-pick/README.md)

<!-- notecardId: 1739477905485 -->

```ts
type Pick<T, K extends keyof T> = {
  [P in K]: T[P];
};
```
